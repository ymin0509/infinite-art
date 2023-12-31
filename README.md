<!DOCTYPE html>
<html>
<head>
    <style>
        /* 공통 스타일 설정 */
        .circle {
            width: 500px;
            height: 500px;
            border-radius: 50%;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-size: cover; /* 이미지 크기 조절 */
            transition: transform 0.2s; /* 부드러운 회전을 위한 트랜지션 설정 */
        </style>
    </head>
    <body>
        <script>
            const commonRatio = 0.8; // 등비 비율
            const numberOfCircles = 10; // 원의 수
            let radius = 250; // 초기 반지름
            let images = ['image1.jpg', 'image2.jpg', 'image3.jpg', 'image4.jpg', 'image5.jpg', 'image6.jpg', 'image7.jpg', 'image8.jpg', 'image9.jpg', 'image10.jpg'];
            let x = 800; // 초기 x 좌표
            let y = 600; // 초기 y 좌표
        
            const circles = [];
        
            const rotationSpeeds = []; // 각 이미지의 회전 속도를 저장할 배열
            for (let i = 0; i < images.length; i++) {
                rotationSpeeds.push(1 + i * 0.2); // 이미지 별로 다른 회전 속도 설정
            }
        
            // image2의 회전 속도를 0.75배로, image3의 회전 속도를 동일하게 설정
            rotationSpeeds[1] = 0.8 * rotationSpeeds[0];
            rotationSpeeds[2] = rotationSpeeds[0];
        
            for (let i = 0; i < numberOfCircles; i++) {
                const circle = document.createElement("div");
                circle.className = "circle";
                circle.style.width = radius * 2 + "px";
                circle.style.height = radius * 2 + "px";
                circle.style.backgroundImage = `url(${images[i % images.length]})`;
                circle.style.left = x ; // 중심이 일치하도록 x 좌표 조정
                circle.style.top = y ; // 중심이 일치하도록 y 좌표 조정
                document.body.appendChild(circle);
                circles.push(circle);
        
                radius *= commonRatio; // 등비수열을 따라 반지름 감소
                x = x ; // 다음 원의 중심을 올바르게 조정
                y = y ; // 다음 원의 중심을 올바르게 조정
            }
        
            // 마우스 위치 이벤트 핸들러
            document.body.addEventListener('mousemove', (event) => {
                const mouseX = event.clientX;
                const mouseY = event.clientY;
                const mouseXDiff = mouseX - window.innerWidth / 2;
                const mouseYDiff = mouseY - window.innerHeight / 2;
                let angleDiff = Math.atan2(mouseYDiff, mouseXDiff) * (180 / Math.PI);
                
                if (angleDiff < 0) {
                    angleDiff += 360; // 각도가 음수이면 360을 더해 0-360 범위로 변환
                }
        
                circles.forEach((circle, index) => {
                    const adjustedAngleDiff = angleDiff * rotationSpeeds[index];
                    circle.style.transform = `translate(-50%, -50%) rotate(${adjustedAngleDiff}deg)`;
                });
            });
        </script>
    </body>
</html>
