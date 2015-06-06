# QAppMemLeak
Small demonstrator of detected memory leak during QApplication (5.4) destruction using address sanitizer (gcc / clang). 

#how to repreduce:
git clone https://github.com/cguentherTUChemnitz/QAppMemLeak
cd ./QAppMemLeak
mkdir build
cd ./build
cmake ../
make
./qappMemLeak

See the memory leak printed by the address sanitizer.
