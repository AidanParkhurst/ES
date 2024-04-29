<script>
    import LightHouse from '$lib/assets/LightHouse.png';
    import Autoretrrato from '$lib/assets/Autorretrato.png';

    let contents;
    let scrolled = 0;
    let vlogLink = "https://streamable.com/e/9vu1sr?";    
    // Rotate the light beams based on the scroll position
    $: angle = scrolled / 10;
    $: screen = Math.floor(angle / 180);

    // Move a spotlight across the screen in line with the beams
    let spotX;
    $:
    if(angle % 360 < 180)
        spotX = - (150 * Math.cos(angle * (Math.PI / 180)));
    else
        spotX = (150 * Math.cos(angle * (Math.PI / 180)));

    // Update z-index of the lighthouse to clarify which beam is in front
    let leftZ;
    let rightZ;
    $:
    if(angle % 180 < 90) {
        leftZ = 0;
        rightZ = 3;
    } else {
        leftZ = 3;
        rightZ = 0;
    }

    // Update the angle of the spotlight to follow the beam
    let spotAngle;
    $:
    if (angle % 360 < 180) {
        spotAngle = (angle+90) + 180;
    } else {
        spotAngle = (angle+90);
    }
</script>

<div class="back">
    {#if angle < 90}
        <h1 class="title">Aidan Parkhurst</h1>
        <p class="title">Desplácese para ver más...</p>
    {:else if (90 < angle) && (angle < 270)}
        <h1 class="title">Ensayo Personal</h1>
    {:else if (270 < angle) && (angle < 450)}
        <h1 class="title">Ensayo Personal (cont.)</h1>
    {:else if (450 < angle) && (angle < 630)}
        <h1 class="title">Algo bobo</h1>
    {:else}
        <h1 class="title">Intereses</h1>
    {/if}
    <img class="lighthouse left" src={LightHouse} style="z-index: {leftZ}" alt="Lighthouse">
    <img class="lighthouse right" src={LightHouse} style="z-index: {rightZ}"alt="Lighthouse">
    <div class="beams" style="transform:rotateY({angle}deg);"></div>
</div>
<div class="scrollable" bind:this={contents}
                        on:scroll={()=>scrolled=contents.scrollTop} >
    <div class="filler" style="min-height: 1510%">
    </div>
</div>
<div class="contents">
    <div class="spot" style="transform:translateX({spotX}%) rotateY({spotAngle}deg)">
        <div class="content">
            {#if screen==0}
                <h1>¡Bienvenidos a mi sitio!</h1>
                <p>Soy Aidan Parkhurst, estudiante, programador, y artista.</p>
                <p>Sigue desplazerse para aprender todo que pueda desear saber de mi</p>
                <p>Empezando con un ensayo personal</p>
            {:else if screen==1}
                <p class="essay">Tengo unas ideas de quién y cómo soy. Pero al mismo tiempo, entiendo y espero que cada persona que interactúa conmigo va a tener su propia versión de mi personalidad, por sus experiencias específicas. Por eso, me gusta decir que soy un hijo, un hermano y un amigo, antes que nada.</p>
                <p class="essay">Aun así, he vivido y experimentado mi propia personalidad, cambiando y aumentando, por 21 años, entonces tengo mi propia opinión de las partes más importantes de mi personalidad. Opino que soy simpático, listo, creativo y detallista. Y para entender porque, necesitamos volver a mi vida hasta ahora.</p>
                <p class="essay">Para empezar, la escuela primaria me dio unos de los mejores años de mi vida, más específicamente, me dio unos de los mejores amigos de toda mi vida. En un tiempo joven, sin muchas dudas, disfruté muchísimo de charlar y pasar tiempo con Patrick, Tomcat y JJ, y todavía hoy les doy crédito para formar mi comportamiento amigable y feliz.</p>
            {:else if screen==2}
                <p class="essay">Por otro lado, el colegio me pasó mucho más difícil. Tenía buenos amigos, y unos maestros genios, pero mis clases eran cien por ciento locos. Recuerdo que en mi primer año, para mi primera tarea en la clase de historia, yo tomé 8 horas para completarla, y recibí una “C“. Estaba destruido, y pensé que había cometido un gran error asistir a una escuela tan desafiante, pero con tiempo, y práctica, aprendí cómo funcionar y de veras, lograr en mi situación estresante. Rodeado de grandes triunfadores, me di cuenta que podría tener esperanzas grandes, y eso me regaló una pasión y dedicación nueva. </p>
                <p class="essay">En todo, mis experiencias en la escuela, y las personas que encontré han formado, más que yo puedo decir, mi manera de ser y mis aspiraciones. Me llevaron a trabajador eficiente y autónomo, y mostraba el valor de amistad y buen humor. Nunca podría dar gracias suficientes por eso, y estoy súper emocionado por continuar aprendiendo y creciendo...</p>
            {:else if screen==3}
                <h1 style="margin-bottom: 10px;">No debo tomarme tan serio, aqui es una presentación más simple de mis intereses:</h1>
                <img class="arte" src={Autoretrrato} alt="Autoretrrato de mi" width="33%">
                <p class="essay">Contiene yo, en el bosque de las latas de Arizona té verde, porque me gustan mucho esas bebidas, y estoy muy enojado que cuestan $1.59 ahora en CityCo. Estoy mirando a mi gato, Mister. Él está brillante porque es la luz de mi vida, y me encanta su barriga. También, él duerme en una cama de Minecraft, porque yo juego muchos videojuegos, y Minecraft es un clásico. Finalmente, hay un patinador haciendo un truco chulo desde mi cabeza, porque pienso el monopatín es divertido.</p>
            {:else if screen==4}
            <iframe allow="fullscreen" allowfullscreen class="video" src="https://streamable.com/e/9vu1sr?"></iframe>
            {:else if screen==5}
                <h1>Me apasionan los videojuegos</h1>
                <p>
                    Me parece un tipo de arte nuevo y podereso. 
                    He creado unos juegos que puedes jugar en tu navegador (solo si no usas movil).
                    Te aviso que Communion es un poco gráfico.
                </p>
                <a target="_blank" href='https://rkhur.st/Wave'>Jugar Wave</a>
                <a target="_blank" href='https://rkhur.st/Communion'>Jugar Communion</a>
            {/if}
        </div>
    </div>
</div>
<style>
    .back {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100%;
        width: 100%;
        position: fixed;
        top: 0;
        left: 0;
        background-color: #022840;
        perspective: 100vw;
    }
    h1.title {
        position: absolute;
        font-family: 'Quicksand';
        color:#F2D750;
        transform: translateY(-33vh);
    }
    p.title {
        position: absolute;
        font-family: 'Quicksand';
        color:#F2D750;
        transform: translateY(-25vh);
    }
    .lighthouse.left {
        position: absolute;
        transform: scale(0.75) translateX(2%) translateY(35%);
        /* only show the left half */
        clip-path: polygon(0 0, 50% 0, 50% 100%, 0 100%);
    }
    .lighthouse.right {
        position: absolute;
        transform: scale(0.75) translateX(2%) translateY(35%);
        /* only show the right half */
        clip-path: polygon(50% 0, 100% 0, 100% 100%, 50% 100%);
    }
    .beams {
        width: 0;
        height: 0;
        border-top: 20vw solid transparent;
        border-bottom: 20vw solid transparent;
        border-right: 50vw solid #F2D750;
        border-left: 50vw solid #F2D750;
    } 

    /* container which detects scrolling anywhere on the page */
    .scrollable {
        height: 100%;
        width: 100%;
        position: absolute;
        top: 0;
        left: 0;
        overflow: scroll;
    }

    /* actual contents of the page */
    .contents {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100%;
        width: 100%;
        position: fixed;
        top: 0;
        left: 0;
        pointer-events: none;
    }
    .spot {
        position: fixed;
        width: 60vw;
        height: 60vw;
        border-radius: 50%;
        background-color: #F2D750;
        z-index: 3;

        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    .content {
        height: 80%;
        width: 75%;
        color: #022840;
        font-family: 'Quicksand';
        
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 20px;
    }
    p {
        text-indent: 20px;
        font-size: larger;
    }
    .essay {
        text-indent: 20px;
        font-size: large;
        margin: 2px;
    }
    .arte {
        margin: 0;
        border-radius: 20px;
    }
    a {
        pointer-events: auto;
        padding: 10px 20px;
        background-color: #022840;
        border: 2px solid #022840;
        color: #F2D750;
        font-size: larger;
        font-weight: bold;
        text-decoration: none;
        border-radius: 20px;
        transition: all 0.3s;
    }
    a:hover {
        background-color: #123850;
    }
    a:active {
        background-color: #F2D750;
        color: #022840;
    }

    /* make the light larger on mobile */
    @media (max-width: 600px) {
        .spot {
            width: 85vh;
            height: 85vh;
        }

        .beams {
            border-top: 20vw solid transparent;
            border-bottom: 20vw solid transparent;
            border-right: 62vw solid #F2D750;
            border-left: 62vw solid #F2D750;
        }
    }

    .video {
        pointer-events: auto;
        border-radius: 20px;
        border: none;
        width: auto;
        height: 80%;
    }

</style>