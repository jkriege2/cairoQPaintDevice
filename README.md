# cairoQPaintDevice
library for Qt: [QPaintDevice](http://doc.qt.io/qt-5/qpaintdevice.html) implementation that uses [Cairo Graphics Library](http://cairographics.org/) as a backend (e.g. for high-quality PDF/EPS/PNG/SVG output!). This library works and was tested with Qt >=4.7, but possibly works with all versions since Qt 4.0!

# License & Previous projects
This project is licensed under the terms of the [GNU General Public License >=3.0](http://www.gnu.org/licenses/gpl-3.0.html).

Parts of this project are based on ideas from the cairo4qt project by ""zgchan...@gmail.com"":
  https://code.google.com/p/cairo4qt/

# Usage
Using this project is simple:
  1. compile the four project-files into your project:
     ```qmake
SOURCES +=  qcairopaintdevice.cpp \
            qcairopaintengine.cpp

HEADERS +=  qcairopaintdevice.h \
            qcairopaintengine.h
	 ```
  2. link your project agains cairo:
     ```qmake
INCLUDEPATH +=  cairo pixman-1
LIBS +=  -lcairo -lpixman-1 -lz -lpng
win32:LIBS += -lgdi32
	 ```
  3. use the newly available QPaintDevice:
     ```c++
// include cairoQPaintDevice header
#include "qcairopaintdevice.h"

// ...

// create paint device to draw to test.pdf, 200x100mm
QCairoPaintDevice * cairoPDF=new QCairoPaintDevice(QSize(200,100), "test.pdf", QCairoPaintDevice::cftPDF);

// paint onto paint device
{
    QPainter p;
    if (p.begin(cairoPDF)) {
        paint(p);
    }
    p.end();
}

// delete paint device and close/finalize file.
delete cairoPDF;
	 ```

	 
