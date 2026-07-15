# Windows

```sh
python -m nuitka ^
  --mode=standalone ^
  --enable-plugin=tk-inter ^
  --include-data-files=tour_assignment_data.json=tour_assignment_data.json ^
  --output-dir=build ^
  --output-filename=TourAssignment.exe ^
  --windows-console-mode=disable ^
  --mingw64 ^
  --assume-yes-for-downloads ^
  tour_assignment_gui.py
```
# Mac

```sh
python -m nuitka \
  --mode=standalone \
  --enable-plugin=tk-inter \
  --include-data-files=tour_assignment_data.json=tour_assignment_data.json \
  --output-dir=build \
  --output-filename=TourAssignment \
  tour_assignment_gui.py
```
