<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Capsulas Emocionales</title>

<style>
    /* colores y tipografía */
    body {
        margin: 0;
        padding: 0;
        font-family: Arial, sans-serif;
        background: #8B0000; /* rojo rubí */
        color: #fff;
        text-align: center;
        display: flex;
        flex-direction: column;
        min-height: 100vh;
    }

    .capa {
        margin: auto;
        max-width: 700px;
        padding: 30px 20px;
        border-radius: 8px;
        background: rgba(0, 0, 0, 0.4);
        display: none;
    }

    .visible {
        display: block;
    }

    .numero {
        font-size: 3rem;
        font-weight: bold;
        color: #000;
    }

    .texto {
        font-size: 1.5rem;
        margin-top: 10px;
        color: #fff;
    }

    .gate {
        margin-top: 20px;
        font-size: 1.2rem;
        color: #fff;
    }

    .audio-final {
        margin-top: 30px;
    }

    button.play {
        padding: 12px 25px;
        font-size: 1rem;
        cursor: pointer;
        border: none;
        border-radius: 5px;
        background: #fff;
        color: #8B0000;
        font-weight: bold;
    }
</style>
</head>

<body>

<!-- 14 capas -->
<div id="capa1" class="capa">
    <div class="numero">01</div>
    <div class="texto">Cuando pienso en ti, mi día se vuelve sol.</div>
</div>

<div id="capa2" class="capa">
    <div class="numero">02</div>
    <div class="texto">Aquí va tu frase para la Capa 02.</div>
</div>

<div id="capa3" class="capa">
    <div class="numero">03</div>
    <div class="texto">Aquí va tu frase para la Capa 03.</div>
</div>

<!-- … hasta capa14 -->
<div id="capa14" class="capa">
    <div class="numero">14</div>
    <div class="texto">Llegamos al final… gracias por estar aquí.</div>

    <!-- Botón para audio final -->
    <div class="audio-final">
        <button class="play" onclick="document.getElementById('audioMensaje').play()">
            ▶ Escuchar mensaje final
        </button>
        <audio id="audioMensaje">
            <source src="mensaje-final.mp3" type="audio/mpeg">
            <!-- Pon aquí tu audio final renombrado -->
        </audio>
    </div>
</div>

<!-- Gate general -->
<div id="gateMensajes" class="capa visible">
    <div class="texto" id="gateTexto"></div>
</div>

<script>
    const ahora = new Date();
    const horaActual = ahora.getHours();
    const minutoActual = ahora.getMinutes();

    // FUNCION QUE DETERMINA SI YA ES LA HORA
    function esHoraDe(hora, minuto) {
        if (horaActual > hora) return true;
        if (horaActual === hora && minutoActual >= minuto) return true;
        return false;
    }

    // CONFIGURACIÓN DE HORAS
    const horarios = [
        {id: "capa1", hora: 9, minuto:14},
        {id: "capa2", hora:10, minuto:14},
        {id: "capa3", hora:11, minuto:14},
        {id: "capa4", hora:12, minuto:14},
        {id: "capa5", hora:13, minuto:14},
        {id: "capa6", hora:14, minuto:14},
        {id: "capa7", hora:15, minuto:14},
        {id: "capa8", hora:16, minuto:14},
        {id: "capa9", hora:17, minuto:14},
        {id: "capa10", hora:18, minuto:14},
        {id: "capa11", hora:19, minuto:14},
        {id: "capa12", hora:20, minuto:14},
        {id: "capa13", hora:21, minuto:14},
        {id: "capa14", hora:22, minuto:14},
    ];

    // ITERAR Y MOSTRAR CAPAS SEGÚN HORA
    let algunaVisible = false;

    for (let i = 0; i < horarios.length; i++) {
        const capaInfo = horarios[i];
        if (esHoraDe(capaInfo.hora, capaInfo.minuto)) {
            document.getElementById(capaInfo.id).classList.add("visible");
            algunaVisible = true;
        }
    }

    // SI NINGUNA CAPA ES VISIBLE, MUESTRA GATE (mensaje de espera)
    if (!algunaVisible) {
        let proxima = horarios.find(h => !esHoraDe(h.hora, h.minuto));
        if (proxima) {
            const gateTexto = document.getElementById("gateTexto");
            gateTexto.textContent = "🔒 La primera capa se desbloquea a las " 
                + String(proxima.hora).padStart(2,"0") + ":" 
                + String(proxima.minuto).padStart(2,"0") + ".";
        }
    } else {
        document.getElementById("gateMensajes").style.display = "none";
    }

</script>

</body>
</html>
