
# Project Title

在 qt-cmake 專案中使用 google test 的範例


## Installation

1. 取得 cmake 專案

```
# clone 專案
git clone https://github.com/smallpig01/gtest_with_qt_cmake.git
# 複製test資料夾至欲測試的專案目錄下
cp -r gtest_with_qt_cmake/test ${dst_test_prj_dir} 
```

2. 修改 CMakeLists.txt 中的 project name 和 google test 路徑
```
# 自訂 專案名稱
set(MY_PROJECT_NAME "gtest_with_cmake")
# 自訂 google test 路徑
set(MY_GOOGLETEST_DIR "googletest")
```

3. QT -> open project -> CMakeLists.txt -> seletct kit -> build
