# $^ pega tudo depois de ":"
# $< pega o primeiro depois de ":"
# $@ pega antes de ":"

# If the first argument is "r"...
ifeq (all,$(firstword $(MAKECMDGOALS)))
  # use the rest as arguments for "r"
  RUN_ARGS := $(wordlist 2,$(words $(MAKECMDGOALS)),$(MAKECMDGOALS))
  # ...and turn them into do-nothing targets
  $(eval $(RUN_ARGS):;@:)
endif
####################################################################
# nessa versao2: usa make all filename_sem_extensao 
# * executa o arquivo especificado e compila todos os arquivos
####################################################################
# se quiser especifica arquivo para execucao somente com make
f= $(RUN_ARGS)

BIB = Linux_IOfiles/io.o
CC = nasm
LD = ld
OBJ_DIR = obj
EXEC_DIR = exec

# pega todos os asm 
# substituir extensao em varios arquivos 
ASM_FILES = $(wildcard *.asm)
OBJ_FILES = $(patsubst %.asm, obj/%.o, $(ASM_FILES))
EXEC_FILES := $(patsubst %.asm, $(EXEC_DIR)/%.out, $(ASM_FILES))
#pega os arquivos.extensao que estao em all, os mesmo acima, estao setados em $@
SRC := %.asm
OBJ := $(OBJ_DIR)/%.o
EXEC := $(EXEC_DIR)/%.out
# ordem de execucao e especifica arquivos usados por %
all: $(OBJ_DIR) $(EXEC_FILES) $(OBJ_FILES) run

#esse primeiro sempre vai ser executado o resto especifica em (all)
# nasm cria os arquivos .o
$(OBJ): $(SRC) 
	$(CC) -f elf -o $@ $< 

# ligador junta o .o no executavel
$(EXEC): $(OBJ) #o arquivo deve existir pra ser target aqui depois de ":"
# $@ pega a origem que no lugar de um nome pra diretiva pode ser $(EXEC)
	$(LD) -m elf_i386 -o $@ $< $(BIB)

# executa e roda - USAR MAKE RUN  é case-sensitive: make run
run: 
	./$(EXEC_DIR)/$(f).out

# cria pastas para arquivos .o e .out caso nao exista
$(OBJ_DIR): 
	@mkdir -p $@ $(EXEC_DIR)

# apaga a pasta obj e o executavel - USAR MAKE CLEAN é case-sensitive: make clean
.PHONY: clean # se tiver um arquivo chamado clean nao da problema
clean:
	@rm -f -r $(OBJ_DIR) $(EXEC_DIR)
#rm -f *.out