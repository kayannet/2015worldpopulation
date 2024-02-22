<script>
    import mapboxgl from 'mapbox-gl';
    import 'mapbox-gl/dist/mapbox-gl.css';
    import { onMount, onDestroy } from 'svelte';
    let map;
    let mapContainer;
    let legend;

    

    mapboxgl.accessToken = "pk.eyJ1Ijoia3F0cmFuIiwiYSI6ImNsc2t6eXQ4czA3dmcyanJ5eWhoaWQxeHIifQ.2kwe8rDh1r-X61ULATh_Jg";
    
    onMount(() => {
        map = new mapboxgl.Map({
                container: mapContainer,
                style: "mapbox://styles/kqtran/clstfey1b000401pt3anhava7" ,  
                center: [-79.035728, 35.932522], // Chapel Hill Public Library
                zoom: 3,
                minZoom: 2,
                maxZoom: 5,
            });
        
        
        map.on('load', () => {
        // the rest of the code will go in here
        
            const layers = [
            '0-3500',
            '3500-7000000',
            '7000000-90000000',
            '90000000-180000000',
            '180000000-300000000',
            '300000000+',
            ];
            const colors = [
            '#ebecd4',
            '#eef1bc',
            '#b6d5a6',
            '#6fbd6b',
            '#93a6a9',
            '#ad8fea',
            ];
        
            // const legend = document.getElementById('legend');
        
            // layers.forEach((layer, i) => {
            //     const color = colors[i];
            //     const item = document.createElement('div')
            //     const key = document.createElement('span');
            //     key.className = 'legend-key';
            //     key.style.backgroundColor = color;
        
            //     const value = document.createElement('span');
            //     value.innerHTML = `${layer}`;
            //     item.appendChild(key);
            //     item.appendChild(value);
            //     legend.appendChild(item)
            // }); 
        
        
            map.on('mousemove', (event) => {
            const countries = map.queryRenderedFeatures(event.point, {
                layers: ['population']
            });
            const population = countries.length ? countries[0].properties.population : undefined;
            document.getElementById('pd').innerHTML = population !== undefined
                ? `<h3>${countries[0].properties.country}</h3><p><strong>${population}</strong> people</p>`
                : `<p>Hover over a country!</p>`;
        });
        
        
            map.getCanvas().style.cursor = 'default';
        
        });
    });
    
    // onDestroy(() => {
    //     map.remove();
    // });
    
    
    
    </script>

    <!-- <div class="map-wrap">
        <div class="map" bind:this={mapContainer} />
    </div> -->
    <main>
        <div class="map-wrap">
            <div class="map" bind:this={mapContainer}></div>
            <div class="map-overlay" id="features">


                <h2>World Population Map (2015) - How does the population of different countries compare?</h2>
                <div id="pd">
                    <p>Hover over a country!</p>
                </div>
            </div>
            <div class="map-overlay" bind:this = {legend} id="legend">
                <!-- Manually created legend key with SVG -->
                <h3>Legend (millions)</h3>
                <svg width="150" height="20">
                    <rect x="0" y="0" width="20" height="20" fill="#ebecd4" />
                    <text x="25" y="15"> &lt; 10 </text>
                </svg>

                <svg width="150" height="20">
                    <rect x="0" y="0" width="20" height="20" fill="#eef1bc" />
                    <text x="25" y="15">10-70</text>
                </svg>

                <svg width="200" height="20">
                    <rect x="0" y="0" width="20" height="20" fill="#b6d5a6" />
                    <text x="25" y="15">70-150</text>
                </svg>

                <svg width="200" height="20">
                    <rect x="0" y="0" width="20" height="20" fill="#6fbd6b" />
                    <text x="25" y="15">150-260</text>
                </svg>

                <svg width="200" height="20">
                    <rect x="0" y="0" width="20" height="20" fill="#93a6a9" />
                    <text x="25" y="15">260-350</text>
                </svg>

                <svg width="150" height="20">
                    <rect x="0" y="0" width="20" height="20" fill="#ad8fea" />
                    <text x="25" y="15">350 &gt;</text>
                </svg>


            </div>
        </div>
    </main>

    onst layers = [
            '0-3500',
            '3500-7000000',
            '7000000-90000000',
            '90000000-180000000',
            '180000000-300000000',
            '300000000+',
            ];
            const colors = [
            '#ebecd4',
            '#eef1bc',
            '#b6d5a6',
            '#6fbd6b',
            '#93a6a9',
            '#ad8fea',
            ];
    
    

  <style>
    body {
        margin: 0;
        padding: 0;
    }
    
    h2,
    h3 {
        margin: 10px;
        font-size: 23px;
    }
    
    h3 {
        font-size: 16px;

    }
    
    p {
        margin: 5px;
        font-size: 20px;
    }
    .map-container {
        width: 100%;
        height: 100%;
        padding: 0;
    }

    .map-wrap {
        position: absolute;
        width: 100%;
        height: 100%; /* Adjust height as needed */
    }
    .map {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        margins: 0;
        padding: 0; /* Ensure no padding */

    }
    
    /**
    * Set rules for how the map overlays
    * (information box and legend) will be displayed
    * on the page. */
    .map-overlay {
        position: absolute;
        bottom: 0;
        right: 0;
        background: #fff;
        margin-right: 25px;
        font-family: Helvectia, sans-serif;
        overflow: auto;
        border-radius: 3px;
        padding: 10px;
    }
    
    #features {
        top: 0;
        height: 160px;
        margin-top: 20px;
        width: 250px;
    }
    
    #legend {
        padding: 15px;
        box-shadow: 0 1px 2px rgba(0 0 0 0.1);
        line-height: 18px;
        /* height: 250px; */
        margin-bottom: 40px;
        width: 200px;
    }
    
    .legend-key {
        display: inline-block;
        border-radius: 20%;
        width: 15px;
        height: 15px;
        margin-right: 5px;
    }
   
  </style>
