<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Sorteo Pro Fondos</title>
  <style>
    body { font-family: Arial; text-align: center; background: #f0f0f0; }
    h1 { color: #222; }
    input { padding: 10px; margin: 5px; }
    button { padding: 10px 20px; background: #4CAF50; color: white; border: none; cursor: pointer; }
    button:hover { background: #45a049; }
    ul { list-style: none; padding: 0; }
    li { background: white; margin: 5px auto; padding: 10px; width: 200px; border-radius: 5px; }
  </style>
</head>
<body>
  <h1>🎉 Sorteo Pro Fondos 🎟️</h1>
  <p>Ingresa tu nombre para participar:</p>
  <input id="nombre" type="text" placeholder="Tu nombre">
  <button id="btnRegistrar">Registrar</button>

  <h2>Participantes</h2>
  <ul id="lista"></ul>

  <!-- Importar Firebase -->
  <script type="module">
    // Tu configuración de Firebase:
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.0.1/firebase-app.js";
    import { getDatabase, ref, push, onValue } from "https://www.gstatic.com/firebasejs/11.0.1/firebase-database.js";

    const firebaseConfig = {
      apiKey: "AIzaSyDTvAbf8W1qfUpV1vXYXpOQk3fUd3EoEeY",
      authDomain: "sorteoprofondos-61b17.firebaseapp.com",
      projectId: "sorteoprofondos-61b17",
      storageBucket: "sorteoprofondos-61b17.firebasestorage.app",
      messagingSenderId: "1160459715",
      appId: "1:1160459715:web:ba7933a073e15233583976",
      measurementId: "G-B55LQ7TR9D",
      databaseURL: "https://sorteoprofondos-61b17-default-rtdb.firebaseio.com"
    };

    const app = initializeApp(firebaseConfig);
    const db = getDatabase(app);

    const inputNombre = document.getElementById("nombre");
    const btnRegistrar = document.getElementById("btnRegistrar");
    const lista = document.getElementById("lista");

    btnRegistrar.addEventListener("click", () => {
      const nombre = inputNombre.value.trim();
      if (nombre) {
        push(ref(db, "participantes"), { nombre });
        inputNombre.value = "";
      }
    });

    onValue(ref(db, "participantes"), (snapshot) => {
      lista.innerHTML = "";
      snapshot.forEach((child) => {
        const li = document.createElement("li");
        li.textContent = child.val().nombre;
        lista.appendChild(li);
      });
    });
  </script>
</body>
</html>
