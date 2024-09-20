<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kuis Gabut</title>
    <style>
        /* Global Style */
        body {
            background-color: #1b1b2f;
            color: #ffffff;
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background-color: #162447;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.5);
            width: 80%;
            max-width: 600px;
        }
        h1 {
            color: #e43f5a;
            text-align: center;
        }
        .form-group {
            margin: 20px 0;
            font-size: 18px;
        }
        input[type="text"], input[type="email"], input[type="tel"] {
            width: 100%;
            padding: 10px;
            margin: 5px 0;
            border: none;
            border-radius: 8px;
            background-color: #1f4068;
            color: #fff;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #e43f5a;
            border: none;
            border-radius: 8px;
            color: white;
            font-size: 18px;
            cursor: pointer;
        }
        button:hover {
            background-color: #f08772;
        }
        .result, .error {
            margin-top: 20px;
            text-align: center;
            font-size: 18px;
        }
        .result {
            color: #00adb5;
        }
        .error {
            color: #f43f5a;
        }
    </style>
</head>
<body>
    <!-- Halaman Registrasi -->
    <div class="container" id="registrationForm">
        <h1>Login Kuis Gabut</h1>
        <div class="form-group">
            <label for="email">Email:</label>
            <input type="email" id="email" placeholder="Masukkan email Anda...">
        </div>
        <div class="form-group">
            <label for="phone">Nomor HP:</label>
            <input type="tel" id="phone" placeholder="Masukkan nomor HP Anda...">
        </div>
        <button type="button" onclick="validateLogin()">Masuk</button>
        <div class="error" id="errorMsg"></div>
    </div>

    <!-- Halaman Kuis -->
    <div class="container" id="quizContainer" style="display: none;">
        <h1>Kuis Kepribadian</h1>
        <form id="quizForm">
            <div class="form-group">
                <label>1. Berapa umur saya?</label>
                <input type="text" id="age" placeholder="Masukkan umurmu...">
            </div>

            <div class="form-group">
                <label>2. Tuliskan nama panjang saya:</label>
                <input type="text" id="fullName" placeholder="Masukkan nama panjang...">
            </div>

            <div class="form-group">
                <label>3. Sebutkan 3 nama panggilan saya:</label>
                <input type="text" id="nicknames" placeholder="Masukkan 3 nama panggilan...">
            </div>

            <div class="form-group">
                <label>4. Sebutkan tanggal, bulan, dan tahun lahir saya:</label>
                <input type="text" id="birthdate" placeholder="Contoh: 25 Februari 2006">
            </div>

            <div class="form-group">
                <label>5. Tanggal 25 Februari 2006 itu hari apa?</label>
                <input type="text" id="birthDay" placeholder="Masukkan hari...">
            </div>

            <div class="form-group">
                <label>Opsional 1: Berapa tinggi badan saya?</label>
                <select id="height">
                    <option value="178">178 cm</option>
                    <option value="168">168 cm</option>
                    <option value="145">145 cm</option>
                    <option value="180">180 cm</option>
                </select>
            </div>

            <div class="form-group">
                <label>Opsional 2: Berapa jumlah mahasiswa TI di UINAM?</label>
                <select id="students">
                    <option value="678">678</option>
                    <option value="390">390</option>
                    <option value="654">654</option>
                    <option value="165">165</option>
                </select>
            </div>

            <div class="form-group">
                <label>Opsional 3: Warna apakah motor yang saya kendarai sehari-hari?</label>
                <select id="motorColor">
                    <option value="biru">Biru</option>
                    <option value="orange">Orange</option>
                    <option value="merah">Merah</option>
                    <option value="hitam">Hitam</option>
                </select>
            </div>

            <button type="button" onclick="checkAnswers()">Kirim Jawaban</button>
        </form>

        <div class="result" id="result"></div>
    </div>


    <script>
        // Validasi login
        function validateLogin() {
            let email = document.getElementById('email').value;
            let phone = document.getElementById('phone').value;
            let errorMsg = document.getElementById('errorMsg');

            if (email === "" || phone === "") {
                errorMsg.textContent = "Email dan nomor HP wajib diisi!";
            } else if (!validateEmail(email)) {
                errorMsg.textContent = "Masukkan format email yang benar!";
            } else {
                document.getElementById('registrationForm').style.display = 'none';
                document.getElementById('quizContainer').style.display = 'block';
            }
        }

        function validateEmail(email) {
            const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            return re.test(email);
        }

        // Cek jawaban kuis
        function checkAnswers() {
            let score = 0;
            let age = document.getElementById('age').value;
            let fullName = document.getElementById('fullName').value.toLowerCase();
            let nicknames = document.getElementById('nicknames').value.toLowerCase();
            let birthdate = document.getElementById('birthdate').value.toLowerCase();
            let birthDay = document.getElementById('birthDay').value.toLowerCase();
            let height = document.getElementById('height').value;
            let students = document.getElementById('students').value;
            let motorColor = document.getElementById('motorColor').value.toLowerCase();

            if (age === "18") score += 10;
            if (fullName === "abd. basith biruni z. bagenda") score += 10;
            if (nicknames.includes("arun") && nicknames.includes("basith") && nicknames.includes("angkasa")) score += 10;
            if (birthdate === "25 februari 2006") score += 10;
            if (birthDay === "sabtu") score += 10;
            if (height === "178") score += 10;
            if (students === "678") score += 10;
            if (motorColor === "biru") score += 10;

            let result = document.getElementById('result');
            result.innerHTML = `Skor kamu: ${score} dari 80 poin!`;
        }
    </script>
</body>
</html>

