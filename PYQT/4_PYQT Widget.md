---
title: PYQT
subtitle: Python GUI Tool
layout: page
show_sidebar: false
menubar: PYQT
---

## PYQT Widget

### QPushButton

버튼에 이벤트 연결하는 방법으로 이벤트에 함수를 연결시켜서 사용한다.

```python
self.[btn_name].clicked.connect(self.[class_function_name])
```

```python
self.Game_start_btn.setEnabled(False) # 버튼 비활성화
self.Game_start_btn.setEnabled(True) # 버튼 활성
```
[https://www.riverbankcomputing.com/static/Docs/PyQt4/qpushbutton.html](https://www.riverbankcomputing.com/static/Docs/PyQt4/qpushbutton.html)

