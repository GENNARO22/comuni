<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8">
  <title>Elenco Comuni Italiani</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; background: #f9f9f9; }
    h1 { color: #2d6a4f; }
    ul { list-style-type: none; padding: 0; }
    li { padding: 5px 0; border-bottom: 1px solid #ccc; }
    input { padding: 10px; width: 300px; margin-bottom: 20px; border: 1px solid #ccc; border-radius: 4px; }
  </style>
</head>
<body>
  <h1>Elenco Comuni Italiani</h1>
  <input type="text" id="searchInput" placeholder="Cerca un comune..." onkeyup="searchComuni()">
  <ul id="comuniList">Caricamento in corso...</ul>

  <script src="comuni.js"></script>
  <script>
    const listElement = document.getElementById('comuniList');
    let allComuni = [];

    function renderList(filtered = allComuni) {
      listElement.innerHTML = "";
      filtered.forEach(comune => {
        const li = document.createElement("li");
        li.textContent = comune;
        listElement.appendChild(li);
      });
    }

    function searchComuni() {
      const input = document.getElementById("searchInput").value.toLowerCase();
      const filtered = allComuni.filter(c => c.toLowerCase().includes(input));
      renderList(filtered);
    }

    document.addEventListener("DOMContentLoaded", () => {
      if (typeof comuniItalia !== "undefined") {
        allComuni = comuniItalia;
        renderList();
      } else {
        listElement.innerHTML = "Errore nel caricamento dei comuni.";
      }
    });
  </script>
</body>
</html>
