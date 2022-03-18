<script>
    import {onMount} from 'svelte';
    import * as THREE from 'three';
	
	let container;

    onMount(() => {
        const scene = new THREE.Scene();
        scene.background = new THREE.Color( 0x1e1f29 );

        const camera = new THREE.PerspectiveCamera( 70, window.innerWidth / window.innerHeight, 0.1, 1000 );

        const renderer = new THREE.WebGLRenderer( { antialias: true } );
        renderer.setSize( window.innerWidth, window.innerHeight);
        
        document.body.appendChild( renderer.domElement );

        const geometry = new THREE.BoxGeometry();
        const edges = new THREE.EdgesGeometry( geometry );
        const line = new THREE.LineSegments( edges, new THREE.LineBasicMaterial( { color: 0xc6afff } ) );
        scene.add( line );
        const material = new THREE.MeshBasicMaterial( { color: 0xc68fff } );
        const cube = new THREE.Mesh( geometry, material );
        scene.add( cube );

        camera.position.z = 2;
        camera.position.y = -0.2;

        const animate = function () {
            requestAnimationFrame( animate );

            cube.rotation.x += 0.02;
            cube.rotation.y += 0.02;

            line.rotation.x += -0.02;
            line.rotation.y += -0.02;

            renderer.render( scene, camera );
        };

        animate();

        function resize() {
            var factor = 1; // percentage of the screen
            var w = window.innerWidth * factor;
            var h = window.innerHeight * factor;
            renderer.setSize(w, h);
            camera.aspect = w / h;
            camera.updateProjectionMatrix();
        }; 

        window.addEventListener("resize", resize);        

    });


</script>

<div bind:this={container}/>
