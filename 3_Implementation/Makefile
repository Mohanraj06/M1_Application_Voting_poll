PROJ_NAME = Library
TEST_PROJ_NAME = Test_$(PROJ_NAME)

BUILD_DIR = BUILD

SRC = src/addBook.c\
src/addDate.c\
src/deleteBook.c\
src/initialised.c\
src/isfileExist.c\
src/isnamevalid.c\
src/isValidDate.c\
src/leap_year.c\
src/login.c\
src/menu.c\
src/searchBook.c\
src/updateCredential.c\
src/viewBook.c\
src/welcomeMessage.c

TEST_SRC = test/test_library.c\
unity/unity.c

INC = -Iinc\
-Iunity

#To check if the OS is Windows or Linux and set the executable file extension and delete command accordingly
ifdef OS
   RM = del /q
   FixPath = $(subst /,\,$1)
   EXEC = exe
else
   ifeq ($(shell uname), Linux)
      RM = rm -rf
      FixPath = $1
	  EXEC = out
   endif
endif

# Makefile will not run target command if the name with file already exists. To override, use .PHONY
.PHONY : all test coverage run clean 

all:$(BUILD_DIR)
	gcc main.c $(SRC) $(INC) -o $(call FixPath,$(BUILD_DIR)/$(PROJ_NAME).$(EXEC))

run: all
	$(call FixPath,$(BUILD_DIR)/$(PROJ_NAME).$(EXEC))

test: $(SRC) $(TEST_SRC)
	gcc $^ $(INC) -o $(call FixPath,$(BUILD_DIR)/$(TEST_PROJ_NAME).$(EXEC))
	$(call FixPath,$(BUILD_DIR)/$(TEST_PROJ_NAME).$(EXEC)) < test/test_input.txt

coverage:${PROJECT_NAME}
	gcc -fprofile-arcs -ftest-coverage $(SRC) $(TEST_SRC) $(INC) -o $(call FixPath,$(BUILD_DIR)/$(TEST_PROJ_NAME).$(EXEC))
	$(call FixPath,$(BUILD_DIR)/$(TEST_PROJ_NAME).$(EXEC)) < test/test_input.txt
	gcov -a $(SRC)
	$(RM) *.gcda 
	$(RM) *.gcno

staticcheck::$(SRC)
	cppcheck --enable=all main.c $(SRC)

memcheck:
	valgrind $(call FixPath,$(BUILD_DIR)/$(TEST_PROJ_NAME).$(EXEC)) < test/test_input.txt

doc:
	make -C doc
$(BUILD_DIR):
	mkdir $(BUILD_DIR)

clean:
	$(RM) $(call FixPath,$(BUILD_DIR)/*)
	$(RM) *.gcda 
	$(RM) *.gcno

# make clean -C doc
# rmdir $(BUILD_DIR) doc/html
