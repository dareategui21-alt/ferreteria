<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FERRETERÍA DR</title>
    <style>
        body { font-family: sans-serif; margin: 0; background: #f0f2f5; padding-bottom: 250px; }
        header { background: #1a4a7a; color: white; text-align: center; padding: 20px; border-bottom: 4px solid #e31e24; }
        .logo-dr { width: 80px; background: white; border-radius: 50%; padding: 5px; }
        
        .seccion-titulo { width: 100%; text-align: center; color: #1a4a7a; font-weight: bold; margin-top: 20px; text-transform: uppercase; }

        /* Contenedor principal */
        #lista-productos { 
            display: flex; flex-wrap: wrap; justify-content: center; 
            gap: 15px; padding: 20px; max-width: 1000px; margin: 0 auto; 
        }
        
        /* Cuadros de productos */
        .tarjeta { 
            background: white; width: 160px; padding: 15px; border-radius: 12px; 
            text-align: center; box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            display: flex; flex-direction: column; justify-content: space-between;
        }
        .img-prod { width: 80px; height: 80px; object-fit: contain; margin: 0 auto; }
        .tarjeta b { font-size: 0.9rem; display: block; height: 35px; overflow: hidden; margin-top: 10px; }
        .precio { color: #e31e24; font-weight: bold; display: block; margin: 10px 0; font-size: 1.2rem; }
        .btn-add { background: #1a4a7a; color: white; border: none; padding: 10px; width: 100%; border-radius: 5px; cursor: pointer; font-weight: bold; }

        /* Footer */
        .footer { position: fixed; bottom: 0; width: 100%; background: white; padding: 15px; text-align: center; box-shadow: 0 -2px 10px rgba(0,0,0,0.1); z-index: 1000; }
        .pagos img { height: 30px; margin: 0 10px; }
        .btn-ws { background: #25D366; color: white; text-decoration: none; padding: 15px; display: block; border-radius: 10px; font-weight: bold; max-width: 300px; margin: 10px auto; }
    </style>
</head>
<body>

<header>
    <img src="garantia.png" class="logo-dr">
    <h1>FERRETERÍA DR</h1>
</header>

<div id="lista-productos">
    <p>Cargando catálogo ampliado...</p>
</div>

<div class="footer">
    <div class="pagos">
        <img src="yape.png">
        <img src="plin.png">
    </div>
    <h3>TOTAL: S/ <span id="monto">0.00</span></h3>
    <a href="#" class="btn-ws" onclick="enviarPedido()">🚀 PEDIR POR WHATSAPP</a>
</div>

<script>
    // LISTA DE PRODUCTOS AMPLIADA
    const misProductos = [
        // Electricidad (Tus originales + nuevos)
        {nombre: "Toma corriente doble", precio: 6.00, img: "https://cdn-icons-png.flaticon.com/512/2802/2802871.png"},
        {nombre: "Interruptor simple", precio: 5.00, img: "https://cdn-icons-png.flaticon.com/512/1041/1041065.png"},
        {nombre: "Foco led 9 watts", precio: 6.00, img: "https://cdn-icons-png.flaticon.com/512/702/702455.png"},
        {nombre: "Cinta aislante", precio: 1.50, img: "https://cdn-icons-png.flaticon.com/512/8226/8226123.png"},
        {nombre: "Socket de loza", precio: 3.50, img: "https://cdn-icons-png.flaticon.com/512/1063/1063319.png"},
        
        // Herramientas
        {nombre: "Martillo de uña", precio: 18.00, img: "https://cdn-icons-png.flaticon.com/512/2505/2505537.png"},
        {nombre: "Wincha 5 metros", precio: 12.00, img: "https://cdn-icons-png.flaticon.com/512/2505/2505504.png"},
        {nombre: "Alicate universal", precio: 15.00, img: "https://cdn-icons-png.flaticon.com/512/2505/2505436.png"},
        {nombre: "Destornillador estrella", precio: 8.00, img: "https://cdn-icons-png.flaticon.com/512/2505/2505471.png"},
        
        // Gasfitería
        {nombre: "Cinta Teflón", precio: 1.50, img: "https://cdn-icons-png.flaticon.com/512/2921/2921474.png"},
        {nombre: "Llave de paso 1/2", precio: 14.00, img: "https://cdn-icons-png.flaticon.com/512/944/944837.png"},
        {nombre: "Tubo PVC 1/2 agua", precio: 9.00, img: "https://cdn-icons-png.flaticon.com/512/3241/3241315.png"}
    ];

    let total = 0;
    let textoWhatsApp = "";

    function render() {
        const contenedor = document.getElementById('lista-productos');
        if (!contenedor) return;
        contenedor.innerHTML = ""; 
        
        misProductos.forEach(p => {
            contenedor.innerHTML += `
                <div class="tarjeta">
                    <img src="${p.img}" class="img-prod">
                    <b>${p.nombre}</b>
                    <span class="precio">S/ ${p.precio.toFixed(2)}</span>
                    <button class="btn-add" onclick="sumar('${p.nombre}', ${p.precio})">AÑADIR</button>
                </div>
            `;
        });
    }

    function sumar(n, p) {
        total += p;
        textoWhatsApp += "- " + n + " (S/ " + p.toFixed(2) + ")%0A";
        document.getElementById('monto').innerText = total.toFixed(2);
    }

    function enviarPedido() {
        if(total === 0) return alert("Por favor, selecciona productos primero");
        const mensaje = "Hola *Ferretería DR*, deseo realizar este pedido:%0A%0A" + textoWhatsApp + "%0A*TOTAL: S/ " + total.toFixed(2) + "*";
        window.open("https://wa.me/51991684812?text=" + mensaje);
    }

    window.onload = render;
</script>

</body>
</html>
