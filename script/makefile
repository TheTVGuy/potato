# ----------------------------------------
#
#  File: makefile
#  Author: Myles Busig
#  Date Created: 2020-05-09
#  Last Edited: 2020-05-13
#
#  Copyright (c) Myles Busig, 2020
#
# ----------------------------------------

# ----------------------------------------
#  Variables
# ----------------------------------------

RWILDCARD = $(wildcard $1/$2) $(foreach DIR,$(wildcard $1/*),$(call RWILDCARD,$(DIR),$2))

# Directories
SRCDIR = src
INCDIR = include
OBJDIR = .obj
DEPDIR = .dep
LIBDIR = .lib
BINDIR = bin

# Files
SRC = $(call RWILDCARD,$(SRCDIR),*.cpp)
OBJ = $(subst $(SRCDIR)/,$(OBJDIR)/,$(SRC:.cpp=.o))
LIB =
BIN = potato_script

# Options
CXX = g++
MKDIR = mkdir -p
RMDIR = rm -r -f
CXXFLAGS = -c -I $(INCDIR) -o $@ $<
LDFLAGS = $^ -L $(LIBDIR) $(addprefix -l,$(LIB)) -o $@
DEPFLAGS = -MM -MG -MP -MF $(subst $(SRCDIR)/,$(DEPDIR)/,$(<:.cpp=.d)) $<

# ----------------------------------------
#  Rules
# ----------------------------------------

# Link objects and libraries
$(BINDIR)/$(BIN) : $(OBJ)
	@$(MKDIR) $(dir $@)
	$(CXX) $(LDFLAGS)

# Compile Sources
$(OBJDIR)/%.o : $(SRCDIR)/%.cpp
	@$(MKDIR) $(dir $@)
	@$(MKDIR) $(dir $(subst $(SRCDIR)/,$(DEPDIR)/,$<))
	@$(CXX) $(DEPFLAGS)
	$(CXX) $(CXXFLAGS)

# Clean all files
clean :
	@$(RMDIR) $(DEPDIR)
	@$(RMDIR) $(OBJDIR)
	@$(RMDIR) $(BINDIR)

# Include dependency files
include $(wildcard $(SRC:.cpp=.d))

# ----------------------------------------
