CC = gcc
CFLAGS = -Wall -Werror -g
LDLIBS = -lcurses

OBJS = cpu.o es.o memoria.o relogio.o console.o instrucao.o err.o \
			 main.o programa.o controle.o so.o irq.o tabpag.o mmu.o processo.o
OBJS_MONT = instrucao.o err.o montador.o
#MAQS = trata_irq.maq init.maq ex1.maq ex2.maq ex3.maq ex4.maq ex5.maq ex6.maq
MAQS = init.maq ex1.maq ex2.maq ex3.maq ex4.maq ex5.maq ex6.maq p1.maq p2.maq p3.maq
TARGETS = main montador ${MAQS}

all: ${TARGETS}

# para gerar o montador, precisa de todos os .o do montador
montador: ${OBJS_MONT}

# para gerar o programa principal, precisa de todos os .o)
main: ${OBJS}

# para transformar um .asm em .maq, precisamos do montador
# monta os programas de usuário no endereço 100
%.maq: %.asm montador
	./montador -e 0 $*.asm > $*.maq

# apaga os arquivos gerados
clean:
	rm -f ${OBJS} ${OBJS_MONT} ${TARGETS} ${MAQS} ${OBJS:.o=.d}

# para calcular as dependências de cada arquivo .c (e colocar no .d)
%.d: %.c
	@set -e; rm -f $@; \
	 $(CC) -MM $(CPPFLAGS) $< > /tmp/$@.$$$$; \
	 sed 's,\($*\)\.o[ :]*,\1.o $@ : ,g' < /tmp/$@.$$$$ > $@; \
	 rm -f /tmp/$@.$$$$

# inclui as dependências
include $(OBJS:.o=.d)
