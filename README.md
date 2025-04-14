# MobileIPCam-Viewer
import cv2
import numpy as np
import urllib.request

# Replace with your phone's IP address and port from the IP Webcam app
# Added "/shot.jpg" to the URL to access the actual image stream
url = "http://'your phone's IP address'/shot.jpg"

while True:
    try:
        # Get the image from the URL
        img_resp = urllib.request.urlopen(url)
        imgnp = np.array(bytearray(img_resp.read()), dtype=np.uint8)
        img = cv2.imdecode(imgnp, -1)
        
        # Check if image was successfully decoded
        if img is None or img.size == 0:
            print("Failed to decode image")
            continue
            
        # Display the image
        cv2.imshow("Phone Camera", img)
        
        # Press 'q' to quit
        if cv2.waitKey(1) & 0xFF == ord('q'):
            break
            
    except Exception as e:
        print(f"Error: {e}")
        # Add a small delay before retrying
        cv2.waitKey(500)

cv2.destroyAllWindows()
