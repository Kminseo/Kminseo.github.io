---
title: PYQT
subtitle: Python GUI Tool
layout: page
show_sidebar: false
menubar: PYQT
---

### PYQT Image Processing
imageLabel.setPixmap\(QtGui.QPixmap.fromImage\(이미지파일\)\)
```python
def get_state(self):
    p = QScreen.grabWindow(app.primaryScreen(), main_dialog.winId())  # (메인화면, 현재위젯)
    p = p.toImage()
    qimg = p.convertToFormat(QImage.Format_RGB888)
    qimg = qimg.rgbSwapped()
    ptr = qimg.constBits()
    ptr.setsize(qimg.byteCount())
    mat = np.array(ptr).reshape(qimg.height(), qimg.width(), 3)
    mat=mat[10:390,10:210] # crop game_image
    mat = cv2.resize(mat, (64, 64))/255
    #cv2.imwrite('Original.jpg', mat)
    print(mat)
    # p.save("test.jpg")
    return mat
```
### PYQT ScreenShot
현재 QT Main Window에 있는 image를 캡쳐합니다.
```python
class MainDialog(QMainWindow):
   def __init__(self):
      QDialog.__init__(self, None) 
      uic.loadUi(CalUI, self)
      self.test_btn.clicked.connect(self.shoot) # 스샷을 찍기위한 함수를 연결

   def shoot(self):
      date = datetime.now()
      filename = date.strftime('%Y-%m-%d_%H-%M-%S.jpg') # 파일이름 만들기용도
      p = QScreen.grabWindow(app.primaryScreen(),main_dialog.winId())#(메인화면, 현재위젯)
      p.save(filename, 'jpg')
      # QScreen은 PYQT5.QtGui에 포함되어 있는 항목으로 grabwindow로 캡쳐가 가능합니다.

if __name__ == "__main__":
   app = QApplication(sys.argv)
   main_dialog = MainDialog()
   main_dialog.show()
   app.exec_()
```