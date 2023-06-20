1.Это задание выполняется на домене attacker.com. Прочитать куки домена attacker.com и вывести их. Попробовать прочитать и вывести куки домена victim.com.

2. Дан сайт, который при нажатии на кнопку меняет цвет фона. Дописать, чтобы при открытии сайта JS обращался в web storage за цветом фона и восстанавливает его.

<body>
<script>
function changeBodyColor(color) {
document.body.style.backgroundColor = color;
}
</script>
<button onclick="changeBodyColor('red')">Make it hell!</button>
<button onclick="changeBodyColor('green')">Make it grass!</button>
</body>


Задание 3. () Самостоятельно настроить CORS на http://victim.com. Разрешить http://localhost с помощью CORS делать запросы к http://victim.com.

Задание 4. () Решить как можно больше XSS на уровне low в bWAPP.