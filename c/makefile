CC=gcc
TARGET_DIR = ./build
TARGET = $(TARGET_DIR)/server $(TARGET_DIR)/client
SERVER_DIR = ./server
CLIENT_DIR = ./client

SOURCE = $(SERVER_DIR)/server.c $(CLIENT_DIR)/client.c

## End sources definition
INCLUDE = 
## end more includes

VPATH=$(SERVER_DIR) $(CLIENT_DIR)
OBJ=$(join $(addsuffix ../obj/, $(dir $(SOURCE))), $(notdir $(SOURCE:.c=.o))) 

## Fix dependency destination to be ../.dep relative to the src dir
DEPENDS=$(join $(addsuffix ../.dep/, $(dir $(SOURCE))), $(notdir $(SOURCE:.c=.d)))

## Default rule executed
all: $(TARGET)
	@true

## Clean Rule
clean:
	@-rm -f $(TARGET) $(OBJ) $(DEPENDS)

## Rule for making the actual target
$(TARGET): $(OBJ)
	@mkdir -p $(dir $@)
	@echo "============="
	@echo "Linking the target $@"
	@echo "============="
	@$(CC) $(CFLAGS) -o $@ $^ $(LIBS)
	@echo -- Link finished --

## Generic compilation rule
%.o : %.c
	@mkdir -p $(dir $@)
	@echo "============="
	@echo "Compiling $<"
	@$(CC) $(CFLAGS) -c $< -o $@


## Rules for object files from cpp files
## Object file for each file is put in obj directory
## one level up from the actual source directory.
../obj/%.o : %.c
	@mkdir -p $(dir $@)
	@echo "============="
	@echo "Compiling $<"
	@$(CC) $(CFLAGS) -c $< -o $@

# Rule for "other directories".
$(SERVER_DIR)/../obj/%.o : %.c
	@mkdir -p $(dir $@)
	@echo "============="
	@echo "Compiling $<"
	@$(CC) $(CFLAGS) -c $< -o $@

$(CLIENT_DIR)/../obj/%.o : %.c
	@mkdir -p $(dir $@)
	@echo "============="
	@echo "Compiling $<"
	@$(CC) $(CFLAGS) -c $< -o $@

## Make dependancy rules
../.dep/%.d: %.c
	@mkdir -p $(dir $@)
	@echo "============="
	@echo Building dependencies file for $*.o
	@$(SHELL) -ec '$(CC) -M $(CFLAGS) $< | sed "s^$*.o^../obj/$*.o^" > $@'

## Dependency rules
$(SERVER_DIR)/../.dep/%.d: %.c
	@mkdir -p $(dir $@)
	@echo "============="
	@echo Building dependency file for $*.o
	@$(SHELL) -ec '$(CC) -M $(CFLAGS) $< | sed "s^$*.o^$(OTHERDIR)/../obj/$*.o^" > $@'

## Dependency rules
$(CLIENT_DIR)/../.dep/%.d: %.c
	@mkdir -p $(dir $@)
	@echo "============="
	@echo Building dependency file for $*.o
	@$(SHELL) -ec '$(CC) -M $(CFLAGS) $< | sed "s^$*.o^$(OTHERDIR)/../obj/$*.o^" > $@'

## Include the dependency files
-include $(DEPENDS)