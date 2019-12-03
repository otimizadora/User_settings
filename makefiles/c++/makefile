SRC_DIR = src
HEADERS_DIR = include
OBJ_DIR = obj
CC = g++
EXE = exe
CFLAGS = -Wall -std=c++11 -I$(HEADERS_DIR)

CPP_FILES = $(wildcard $(SRC_DIR)/*.cpp)
# notdir tira caminho (pastas) do arquivo 
# addprefix add algo na frente de uma word, contrariamente: $(addsuffix .c,foo bar)
OBJ_FILES = $(addprefix $(OBJ_DIR)/,$(notdir $(CPP_FILES:.cpp=.o)))
HPP_FILES = $(wildcard $(HEADERS_DIR)/*.hpp)


all: obj_dir compile


#cria os arquivos .o
$(OBJ_DIR)/%.o : $(SRC_DIR)/%.cpp $(HPP_FILES)
	$(CC) -c -o $@ $< $(CFLAGS)

#junta os .o em um arquivo executavel
compile: $(OBJ_FILES)
	$(CC) -o $(EXE) $^ $(CFLAGS)

#cria a pasta para os arquivos .o caso nao exista
obj_dir :
	mkdir -p $(OBJ_DIR)

#compila e roda o programa
run : all
	./$(EXE)

#deleta a pasta dos arquivos .o e o executavel
clean :
	rm -f -r $(OBJ_DIR)
	rm -f $(EXE)