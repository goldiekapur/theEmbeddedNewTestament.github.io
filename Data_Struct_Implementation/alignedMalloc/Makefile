CC=gcc
CFLGAS=-Wall
OBJ = memalign_new

%.o: %.c
	$(CC) -c -o $@ $< $(CFLAGS)

$(OBJ): $(OBJ).o
	$(CC) -o $@ $^ $(CFLAGS)

clean:
	rm -f $(OBJ) $(OBJ).o
