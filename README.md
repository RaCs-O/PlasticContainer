<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Inventario</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 30px;
    }
    input {
      padding: 8px;
      font-size: 16px;
      width: 300px;
    }
    table {
      margin-top: 20px;
      border-collapse: collapse;
      width: 100%;
    }
    th, td {
      padding: 8px;
      border: 1px solid #ccc;
      text-align: left;
    }
    th {
      background-color: #f2f2f2;
    }
  </style>
</head>
<body>
  <h1>Inventario</h1>
  <input type="text" id="busqueda" placeholder="Buscar por código..." />

  <table id="resultados" style="display:none;">
    <thead>
      <tr>
        <th>Código</th>
        <th>Descripción</th>
        <th>Cantidad</th>
        <th>Ubicación</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>

  <script>
    const inventario = [
      { codigo: "1001005NA", descripcion: "chacis de carro", cantidad: 1, ubicacion: "p2 n2" },
      { codigo: "2002005NA", descripcion: "pieza plana en forma rectangular con 8 puntos de anclaje", cantidad: 2, ubicacion: "p2 n2" },
      { codigo: "2003005NA", descripcion: "pieza plana rectangular chica de 2 puntos de anclaje", cantidad: 11, ubicacion: "Caja 1" },
      { codigo: "2004005NA", descripcion: "pieza plana en forma de L de 3 puntos de anclaje", cantidad: 6, ubicacion: "Caja 1" },
      { codigo: "2005005NA", descripcion: "pieza plana cuadrada de 4 puntos de anclaje", cantidad: 5, ubicacion: "Caja 1" },
      { codigo: "2006005NA", descripcion: "pieza plana rectangular alargada de 4 puntos de anclaje", cantidad: 3, ubicacion: "Caja 1" },
      { codigo: "2007005NA", descripcion: "pieza plana de 1 punto de anclaje", cantidad: 8, ubicacion: "Caja 1" },
      { codigo: "2008005NA", descripcion: "pieza plana rectangular de 6 puntos de anclaje", cantidad: 4, ubicacion: "Caja 1" },
      { codigo: "2009005NA", descripcion: "pieza plana alargada de 6 puntos de anclaje", cantidad: 1, ubicacion: "Caja 1" },
      { codigo: "2010005NA", descripcion: "pieza plana de 1 punto de anclaje transparente", cantidad: 2, ubicacion: "Caja 1" },
      { codigo: "3011005NA", descripcion: "pieza plana lisa de color rojo de 1 puerto de anclaje", cantidad: 2, ubicacion: "Caja 2" },
      { codigo: "3012005NA", descripcion: "pieza plana liza en forma de pico", cantidad: 2, ubicacion: "Caja 2" },
      { codigo: "3013005NA", descripcion: "pieza plana liza en forma de pico", cantidad: 2, ubicacion: "Caja 2" },
      { codigo: "3014005NA", descripcion: "pieza liza en forma de rampa con 1 puerto de anclaje color rojo", cantidad: 2, ubicacion: "Caja 2" },
      { codigo: "3015005NA", descripcion: "pieza liza en forma de rampa con 2 puertos de anclaje color negro", cantidad: 3, ubicacion: "Caja 2" },
      { codigo: "3016005NA", descripcion: "pieza liza con una curba asia adelante con 4 puertos de anclaje en escalon", cantidad: 4, ubicacion: "Caja 2" },
      { codigo: "3017005NA", descripcion: "pieza liza en forma de rampa con un puerto de anclaje color negro", cantidad: 6, ubicacion: "Caja 2" },
      { codigo: "3018005NA", descripcion: "pieza liza cuadrada color negro con 4 puertos de anclaje", cantidad: 1, ubicacion: "Caja 2" },
      { codigo: "3019005NA", descripcion: "pieza liza con una curva asia adelante color negro con un logo inpreso de cuatro puertos de anclaje", cantidad: 2, ubicacion: "Caja 2" },
      { codigo: "3020005NA", descripcion: "pieza liza en forma de arco con un estampado", cantidad: 2, ubicacion: "Caja 2" },
      { codigo: "3021005NA", descripcion: "pieza liza alargada con una curba asia adelate de una sola fila de puertos de anclaje", cantidad: 2, ubicacion: "Caja 2" },
      { codigo: "3022005NA", descripcion: "pieza liza con una curva asia adelante color negro con un dos lineas rojas inpreso de cuatro puertos de anclaje", cantidad: 1, ubicacion: "Caja 2" },
      { codigo: "3023005NA", descripcion: "pieza liza alargada chica con una curva asia adelante con dos puertos de anclaje", cantidad: 2, ubicacion: "Caja 2" },
      { codigo: "3024005RH", descripcion: "pieza plana liza en forma de pico color negro", cantidad: 1, ubicacion: "Caja 2" },
      { codigo: "3025005LH", descripcion: "pieza plana liza en forma de pico color negro", cantidad: 1, ubicacion: "Caja 2" },
      { codigo: "3026005NA", descripcion: "pieza liza con un logo estampado", cantidad: 1, ubicacion: "Caja 2" },
      { codigo: "3027005NA", descripcion: "pieza liza con una curba asia adelante con dos lineas rojas que llegan a la mitad de la pieza", cantidad: 1, ubicacion: "Caja 2" },
      { codigo: "3028005NA", descripcion: "pieza liza en forma de rampa transparente con 1 puerto de anclaje", cantidad: 2, ubicacion: "Caja 2" },
      { codigo: "3029005NA", descripcion: "pieza liza en forma de rampa con 2 puertos de anclaje de color gris", cantidad: 1, ubicacion: "Caja 2" },
      { codigo: "3030005NA", descripcion: "pieza liza de color negre de 6 puertos de anclaje", cantidad: 1, ubicacion: "Caja 2" },
      { codigo: "3031005NA", descripcion: "pieza liza en forma de L con la esquina cortada", cantidad: 2, ubicacion: "Caja 2" },
      { codigo: "3032005NA", descripcion: "pieza liza alargada de color negro con una curba asia adelate de una sola fila de puertos de anclaje", cantidad: 2, ubicacion: "Caja 2" },
      { codigo: "4033005NA", descripcion: "pieza en forma de L vertical con 2 puertos de anclaje y 4 puntos de anclaje", cantidad: 4, ubicacion: "Caja 3" },
      { codigo: "4034005NA", descripcion: "pieza cuadrada con un escalon y un pequeño eje en un extremo", cantidad: 4, ubicacion: "Caja 3" },
      { codigo: "4035005NA", descripcion: "pieza de un solo puerto de anclaje con dos paredes en forma de L", cantidad: 2, ubicacion: "Caja 3" },
      { codigo: "4036005NA", descripcion: "pieza en forma de volante de auto", cantidad: 1, ubicacion: "p2 n1" },
      { codigo: "4037005NA", descripcion: "piesa con 4 puntos de anclaje con un escalon con un arco en un extremo", cantidad: 4, ubicacion: "Caja 3" },
      { codigo: "4038005NA", descripcion: "pieza cubica con un saliente en su parte inferior un punto de anclaje arriba y uno en un extremo", cantidad: 4, ubicacion: "Caja 3" },
      { codigo: "4039005NA", descripcion: "pieza de 2 puntos de anclaje con 2 ganchos en un extremo", cantidad: 1, ubicacion: "Caja 3" },
      { codigo: "4040005NA", descripcion: "pieza en forma de L vertical con 2 puertos de anclaje y 4 puntos de anclaje( invertida )", cantidad: 3, ubicacion: "Caja 3" },
      { codigo: "4041005NA", descripcion: "pieza cubica con 1 punto de anclaje arriba y uno en un extremo los puntos son huecos", cantidad: 4, ubicacion: "Caja 3" },
      { codigo: "4042005NA", descripcion: "piesa en forma de rampa en el sentro es escalonada de color rojo", cantidad: 2, ubicacion: "Caja 3" },
      { codigo: "4043005NA", descripcion: "pieza con un punto de anclaje y un eje orizontal con dos puntos de anclajes huecos", cantidad: 2, ubicacion: "Caja 3" },
      { codigo: "4044005NA", descripcion: "pieza con 2 puertos de anclaje con un perfil en un extremo", cantidad: 2, ubicacion: "Caja 3" },
      { codigo: "4045005NA", descripcion: "pieza cubica con un punto de anclaje", cantidad: 2, ubicacion: "Caja 3" },
      { codigo: "4046005NA", descripcion: "pieza de 2 puntos de anclaje huecos y un puerto de anclaje de forma horizontal", cantidad: 2, ubicacion: "Caja 3" },
      { codigo: "4047005NA", descripcion: "pieza de 2 puntos de anclaje y un anclaje vertical", cantidad: 1, ubicacion: "Caja 3" },
      { codigo: "4048005NA", descripcion: "pieza en forma de rampa alargada con dos puntos de anclaje huecos en el lugar de los puertos", cantidad: 2, ubicacion: "Caja 3" },
      { codigo: "4049005NA", descripcion: "pieza liza con un puerto de anclaje con la esquina redondeada", cantidad: 2, ubicacion: "Caja 3" },
      { codigo: "4050005NA", descripcion: "piesa en forma de rampa en el sentro es escalonada de color negro", cantidad: 2, ubicacion: "Caja 3" },
      { codigo: "4051005NA", descripcion: "pieza en forma de L en vertical con dos abrasaderas a los costados", cantidad: 1, ubicacion: "Caja 3" },
      { codigo: "4052005RH", descripcion: "pieza cuadrada con una esquina cortada de color rojo transparente con tres puertos de anclaje", cantidad: 1, ubicacion: "Caja 3" },
      { codigo: "4053005LH", descripcion: "pieza cuadrada con una esquina cortada de color rojo transparente con tres puertos de anclaje", cantidad: 1, ubicacion: "Caja 3" },
      { codigo: "4054005NA", descripcion: "pieza en forma de aleron pequeño", cantidad: 3, ubicacion: "Caja 3" },
      { codigo: "4055005NA", descripcion: "pieza cilindrica con un hueco en el centro(rin de rueda)", cantidad: 4, ubicacion: "p3 n1" },
      { codigo: "4056005NA", descripcion: "pieza circular con un hueco muy grande en el centro en el exterior tiene dientes (rueda de carro )", cantidad: 4, ubicacion: "p2 n1" },
      { codigo: "4057005NA", descripcion: "piesa grande en forma de rampa curviada asia adelante transparente ( para brisas de carro)", cantidad: 1, ubicacion: "p2 n1" }
    ];

    const input = document.getElementById("busqueda");
    const tabla = document.getElementById("resultados");
    const tbody = tabla.querySelector("tbody");

    input.addEventListener("input", () => {
      const valor = input.value.trim().toLowerCase();
      tbody.innerHTML = "";
      if (valor === "") {
        tabla.style.display = "none";
        return;
      }
      const resultados = inventario.filter(item => item.codigo.toLowerCase().includes(valor));
      resultados.forEach(item => {
        const fila = document.createElement("tr");
        fila.innerHTML = `
          <td>${item.codigo}</td>
          <td>${item.descripcion}</td>
          <td>${item.cantidad}</td>
          <td>${item.ubicacion}</td>
        `;
        tbody.appendChild(fila);
      });
      tabla.style.display = resultados.length ? "table" : "none";
    });
  </script>
</body>
</html>
