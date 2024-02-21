<!DOCTYPE html>
<html lang="fr">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Plan de Révision</title>
    <style>
        body {
            background-color: black;
            color: grey;
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }

        #container {
            max-width: 600px;
            margin: 0 auto;
        }

        input {
            padding: 10px;
            margin: 10px 0;
        }

        button {
            padding: 10px 20px;
            background-color: grey;
            color: black;
            border: none;
            cursor: pointer;
        }

        #output {
            margin-top: 20px;
        }

        .revision {
            font-weight: bold;
            color: red;
        }
    </style>
</head>

<body>
    <div id="container">
        <h1 style="color: red;">Plan de Révision</h1>
        <label for="date">Date du Contrôle :</label>
        <input type="date" id="date">

        <button onclick="planifier()">Planifier</button>

        <div id="output"></div>
    </div>

    <script>
        function planifier() {
            var dateInput = document.getElementById("date");
            var dateControle = new Date(dateInput.value);
            var today = new Date();

            var diffDays = Math.floor((dateControle - today) / (1000 * 60 * 60 * 24));

            if (diffDays < 0) {
                document.getElementById("output").innerHTML = "La date du contrôle doit être dans le futur.";
            } else {
                var seances = [diffDays - 1, diffDays - 2, diffDays - 4, diffDays - 7, diffDays - 11, diffDays - 16, diffDays - 22, diffDays - 29, diffDays - 37, diffDays - 46, diffDays - 56, diffDays - 67, diffDays - 78, diffDays - 89];
                var outputHTML = "<h2>Plan de Révision</h2>";

                for (var i = seances.length - 1; i >= 0; i--) {
                    if (seances[i] >= 0) {
                        var seanceDate = new Date(today);
                        seanceDate.setDate(today.getDate() + seances[i]);
                        var formattedDate = seanceDate.toLocaleDateString('fr-FR');
                        outputHTML += "<p>" + (seances.length - i) + ": <span class='revision'>" + formattedDate + "</span></p>";
                    }
                }

                document.getElementById("output").innerHTML = outputHTML;
            }
        }
    </script>
</body>

</html>

