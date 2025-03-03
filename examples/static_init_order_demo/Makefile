# https://isocpp.org/wiki/faq/ctors#static-init-order

FLAGS = -std=c++17 -Og -g3 -Wall -fsanitize=address
ASAN_OPTIONS = check_initialization_order=true

define run_demo
$(CXX) $(FLAGS) -c file1.cpp -o file1.o ;\
$(CXX) $(FLAGS) -c file2.cpp -o file2.o ;\
$(CXX) $(FLAGS) file2.o file1.o -o file21.exe ;\
$(CXX) $(FLAGS) file1.o file2.o -o file12.exe ;\
\
echo -n "Option A: Link file2.cpp then file1.cpp\n    " ;\
./file21.exe ;\
\
echo -n "\nOption B: Link file1.cpp then file2.cpp\n    " ;\
./file12.exe ;\
\
echo -n "\nOption B (with -fsanitize=address and ASAN_OPTIONS=$(ASAN_OPTIONS))\n" ;\
ASAN_OPTIONS=$(ASAN_OPTIONS) ./file12.exe ;\
\
rm -f *.exe *.o
endef

.PHONY: all
all:
	@$(run_demo)
