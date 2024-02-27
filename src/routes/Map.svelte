<!-- Map.svelte -->
<script>
    import { onMount } from 'svelte';
    import 'ol/ol.css'; // Import OpenLayers CSS
    import Map from 'ol/Map';
    import View from 'ol/View';
    import TileLayer from 'ol/layer/Tile';
    import OSM from 'ol/source/OSM';
    import { Draw } from 'ol/interaction';
    import { Vector as VectorSource } from 'ol/source';
    import { Vector as VectorLayer } from 'ol/layer';
    import { Style, Fill, Stroke, Text } from 'ol/style';
  
    import Modal from './Modal.svelte'; // Import your modal component
  
    let map;
    let draw;
    let type = 'Polygon';
    let showModal = false;
  
    onMount(() => {
        const raster = new TileLayer({
            source: new OSM(),
        });
  
        const source = new VectorSource({ wrapX: false });
  
        const vector = new VectorLayer({
            source: source,
        });
  
        map = new Map({
            layers: [raster, vector],
            target: 'map',
            view: new View({
                center: [-11687603.768526185, 4828527.173843127],
                zoom: 12,
            }),
        });
  
        addInteraction();
    });
  
    function addInteraction() {
        if (type !== 'None') {
            draw = new Draw({
                source: map.getLayers().getArray()[1].getSource(),
                type: type,
            });
  
            draw.on('drawend', function(event) {
                showModal = true; // Show the modal
                draw.feature = event.feature; // Pass the drawn feature to modal
            });
  
            map.addInteraction(draw);
        }
    }
  
    function handleTypeChange(event) {
        type = event.target.value;
        map.removeInteraction(draw);
        addInteraction();
    }
  
    function handleUndo() {
        draw.removeLastPoint();
    }
  
    function handleCloseModal() {
        showModal = false;
    }
  
    function handleSaveModal(event) {
        const { name, description } = event.detail;
        showModal = false;
        const feature = draw.feature;
        feature.setProperties({
            'name': name,
            'description': description
        });
  
        const fillStyle = new Fill({
            color: 'rgba( 221, 49, 12 , 0.2)'
        });
  
        const strokeStyle = new Stroke({
            color: 'black',
            width: 2
        });
  
        feature.setStyle(new Style({
            fill: fillStyle,
            stroke: strokeStyle
        }));
  
        const textStyle = new Text({
            font: '14px Calibri,sans-serif',
            fill: new Fill({
                color: '#000'
            }),
            stroke: new Stroke({
                color: '#fff',
                width: 2
            }),
            text: name,
            offsetX: 0,
            offsetY: 10,
        });
  
        feature.getStyle().setText(textStyle);
    }
  </script>
  
  <div id="map" style="width: 100%; height: 100%;"></div>
  
  <Modal {showModal} onClose={handleCloseModal} on:save={handleSaveModal} />
  