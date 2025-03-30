# TD
برای برانامه ریزی روزانه
<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>برنامه روزانه</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f4;
            color: #333;
            direction: rtl;
            transition: background 0.3s, color 0.3s;
        }
        .container {
            width: 80%;
            margin: auto;
            padding: 20px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .dark-mode {
            background-color: #222;
            color: white;
        }
        .btn {
            margin: 10px;
            padding: 10px 20px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
        }
        .btn-dark {
            background: black;
            color: white;
        }
        textarea {
            width: 100%;
            height: 200px;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <button class="btn btn-dark" onclick="toggleDarkMode()">تغییر تم</button>
    <button class="btn" onclick="generateSchedule()">تولید برنامه روزانه</button>
    <div class="container">
        <h1>برنامه روزانه شما</h1>
        <h2>روزهای عادی</h2>
        <ul id="daily-schedule">
        </ul>
        <h2>روزهای تعطیل</h2>
        <ul id="holiday-schedule">
        </ul>
    </div>
    <script>
        function toggleDarkMode() {
            document.body.classList.toggle("dark-mode");
        }

        function generateSchedule() {
            const dailySchedule = [
                "۶:۰۰ صبح - بیدار شدن و آماده‌سازی روزانه",
                "۷:۰۰ تا ۱۳:۳۰ - مدرسه",
                "۱۵:۰۰ تا ۱۶:۳۰ - مطالعه و تکالیف",
                "۱۶:۳۰ تا ۱۷:۳۰ - بازی و تفریح",
                "۱۸:۰۰ تا ۱۹:۰۰ - ورزش و ۱۰۰ شنا",
                "۱۹:۰۰ تا ۱۹:۳۰ - مطالعه ۱۰ صفحه کتاب"
            ];

            const holidaySchedule = [
                "۸:۳۰ - بیدار شدن",
                "۹:۰۰ تا ۱۰:۰۰ - یادگیری شخصی",
                "۱۰:۰۰ تا ۱۱:۰۰ - ورزش و شنا",
                "۱۶:۳۰ تا ۱۷:۳۰ - بازی یا تفریح",
                "۱۹:۰۰ تا ۱۹:۳۰ - مطالعه ۱۰ صفحه دیگر کتاب"
            ];

            document.getElementById("daily-schedule").innerHTML = dailySchedule.map(item => `<li>${item}</li>`).join('');
            document.getElementById("holiday-schedule").innerHTML = holidaySchedule.map(item => `<li>${item}</li>`).join('');
        }
    </script>
</body>
</html>
