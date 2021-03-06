# Reference: https://spin.atomicobject.com/2016/08/26/makefile-c-projects/ for assistance with make file.

CC = gcc
TARGET_EXEC ?= writer

BIN_DIR ?= .
BUILD_DIR ?= ./build
SRC_DIRS ?= .

SRCS := $(shell find $(SRC_DIRS) -name '*.c' -or -name '*.cpp' -or -name '*.s')
OBJS := $(SRCS:%=$(BUILD_DIR)/%.o)
DEPS := $(OBJS:.o=.d)

INC_DIRS := $(shell find $(SRC_DIRS) -type d)
INC_FLAGS := $(addprefix -I,$(INC_DIRS))

CPPFLAGS ?= $(INC_FLAGS) -g -Wall -Werror


$(BIN_DIR)/$(TARGET_EXEC): $(OBJS)
	$(MKDIR_P) $(BIN_DIR)
	$(CROSS_COMPILE)$(CC) $(OBJS) -o $@ $(LDFLAGS)

# assembly
# $(BUILD_DIR)/%.s.o: %.s
# 	$(MKDIR_P) $(dir $@)
# 	$(AS) $(ASFLAGS) -c $< -o $@

# c source
$(BUILD_DIR)/%.c.o: %.c
	$(MKDIR_P) $(dir $@)
	$(CROSS_COMPILE)$(CC) $(CPPFLAGS) $(CFLAGS) -c $< -o $@

# c++ source
# $(BUILD_DIR)/%.cpp.o: %.cpp
# 	$(MKDIR_P) $(dir $@)
# 	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $< -o $@


.PHONY: clean

clean:
	$(RM) -r $(BUILD_DIR)
	$(RM) -f $(TARGET_EXEC)

-include $(DEPS)

MKDIR_P ?= mkdir -p
