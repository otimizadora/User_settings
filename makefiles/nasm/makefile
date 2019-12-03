# $^ pega tudo depois de ":"
# $< pega o primeiro depois de ":"
# $@ pega antes de ":"

# If the first argument is "r"...
ifeq (r,$(firstword $(MAKECMDGOALS)))
  # use the rest as arguments for "r"
  RUN_ARGS := $(wordlist 2,$(words $(MAKECMDGOALS)),$(MAKECMDGOALS))
  # ...and turn them into do-nothing targets
  $(eval $(RUN_ARGS):;@:)
endif
####################################################################
# usar make f=filename_sem_extensao ou  make r filename_sem_extensao
####################################################################
# se quiser especifica arquivo para leitura somente com make
f= $(RUN_ARGS)

BIB = Linux_IOfiles/io.o
CC = nasm
LD = ld
OBJ_DIR = obj

# extensoes
# outra para substituir varios arquivos em src := $(patsubst %.cpp, obj/%.o, $(SRC))
SRC := $(f).asm
OBJ := $(OBJ_DIR)/$(SRC:.asm=.o)
EXEC := $(SRC:.asm=.out)

# ordem de execucao
r: $(OBJ_DIR) $(EXEC) run clean

#esse primeiro sempre vai ser executado o resto especifica em r (all)
# nasm cria os arquivos .o
$(OBJ): $(SRC) 
	$(CC) -f elf -o $@ $< 

# ligador junta o .o no executavel
$(EXEC): $(OBJ) $(BIB) #o arquivo deve existir pra ser target aqui depois de ":"
# $@ pega a origem que no lugar de um nome pra diretiva pode ser $(EXEC)
	$(LD) -m elf_i386 -o $@ $^ 

# executa e roda - USAR MAKE RUN  é case-sensitive: make run
run: 
	./$(EXEC)

# cria pasta para arquivos .o caso nao exista
$(OBJ_DIR):
	@mkdir -p $@

# apaga a pasta obj e o executavel - USAR MAKE CLEAN é case-sensitive: make clean
.PHONY: clean # se tiver um arquivo chamado clean nao da problema
clean:
	@rm -f -r $(OBJ_DIR)
	@rm -f $(EXEC)

