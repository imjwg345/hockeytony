import cv2
import mediapipe as mp
import math

mp_face_mesh = mp.solutions.face_mesh
face_mesh = mp_face_mesh.FaceMesh()

cap = cv2.VideoCapture(0)
cv2.namedWindow("Eye Tracking")

# 화면 크기
screen_width, screen_height = 640, 480

# 점 초기 위치 (화면 중심)
            # 화면 중심을 기준으로 점 이동
            if horizontal_direction == "Look Left":
                point_x -= 10
            elif horizontal_direction == "Look Right":
                point_x += 10

            if vertical_direction == "Look Up":
                point_y -= 10
            elif vertical_direction == "Look Down":
                point_y += 10

            # 화면 중심을 기준으로 십자 모양 이동 제한
            if abs(point_x - screen_width // 2) > abs(point_y - screen_height // 2):
                point_y = screen_height // 2
            else:
                point_x = screen_width // 2

            # 화면 끝까지만 이동 가능하도록 제한
            point_x = max(0, min(point_x, screen_width))
            point_y = max(0, min(point_y, screen_height))

            cv2.circle(image, (point_x, point_y), 5, (0, 255, 0), -1)

    cv2.imshow("Eye Tracking", image)

    if cv2.waitKey(5) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
