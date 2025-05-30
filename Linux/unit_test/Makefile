# Copyright (C) 2022-2023 Arm Technology (China) Co. Ltd. All rights reserved.
#
# SPDX-License-Identifier: Apache-2.0

TARGET := runtime_unit_test
#CXX = aarch64-linux-gnu-g++
#CXX = g++
RM  := rm -rf
MV  := mv
RUNTIME_SRC_PATH := ../driver/umd/src
RUNTIME_TEST_SRC_PATH := .
TEST_UNIT +=  .
TEST_UNIT += context
TEST_UNIT += graph
TEST_UNIT += parser
TEST_UNIT += job
SRC_UNIT += device/aipu
ifeq ($(BUILD_TARGET_PLATFORM), sim)
	SRC_UNIT += device/simulator
endif
SRC_UNIT += utils
SRC_UNIT += common
SRC_UNIT += zhouyi_v1v2
SRC_UNIT += zhouyi_v3
SRC_UNIT += .
SRC_UNIT += $(DEVICE_SRC)

RUNTIMR_SRCS_SECTION  :=
RUNTIMR_TEST_SECTION  :=
RUNTIME_HEADER_PATH   :=
RUNTIMR_TEST_SECTION += $(foreach VAR, $(TEST_UNIT), $(wildcard $(RUNTIME_TEST_SRC_PATH)/$(VAR)/*.cpp))
RUNTIMR_TEST_HEADER_PATH += -I.
RUNTIMR_SRCS_SECTION += $(foreach VAR, $(SRC_UNIT), $(wildcard $(RUNTIME_SRC_PATH)/$(VAR)/*.cpp))
RUNTIME_HEADER_PATH += $(foreach VAR, $(SRC_UNIT), -I$(RUNTIME_SRC_PATH)/$(VAR))
RUNTIME_HEADER_PATH += -I../driver/umd/src
RUNTIME_HEADER_PATH += -I../driver/umd/include
RUNTIME_HEADER_PATH += -I../driver/umd/include/kmd
RUNTIME_HEADER_PATH += -I../driver/umd/include/simulator
RUNTIME_HEADER_PATH += -I../driver/umd/src/device/
RUNTIME_HEADER_PATH += -I../driver/umd/src/device/aipu
RUNTIME_HEADER_PATH += -I../driver/umd/src/device/simulator
RUNTIME_HEADER_PATH += -I../driver/umd/src/utils
RUNTIME_HEADER_PATH += -I../driver/umd/src/common
RUNTIME_HEADER_PATH += -I../driver/umd/src/zhouyi_v1v2
RUNTIME_HEADER_PATH += -I../driver/umd/src/zhouyi_v3
RUNTIME_HEADER_PATH += -I../driver/umd/3rdparty
RUNTIME_HEADER_PATH += -I../driver/umd/3rdparty/elfio
RUNTIME_HEADER_PATH += -I../driver/umd/3rdparty/numpy

ifeq ($(BUILD_TARGET_PLATFORM), sim)
	LDFLAGS := -L$(CONFIG_DRV_BRENVAR_X2_SIM_LPATH) -l$(COMPASS_DRV_BRENVAR_X2_SIM_LNAME)
endif

SRCS := $(wildcard $(RUNTIME_TEST_SRC_PATH)/*.cpp)
SRCS += $(RUNTIMR_SRCS_SECTION)
SRCS += $(RUNTIMR_TEST_SECTION)
OBJS := $(patsubst %cpp, %o, $(SRCS))
LDFLAGS += -lpthread
CXXFLAGS := -g -Wall  -std=c++14  ${RUNTIME_HEADER_PATH}  ${RUNTIMR_TEST_HEADER_PATH}

all: $(TARGET)
$(TARGET): $(OBJS)
	$(CXX) $^ $(LDFLAGS) -o $@
	$(RM) $(OBJS)
%.o: %.cpp
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $< -o $@
clean:
	$(RM) $(OBJS) $(TARGET)
test:
	$(CXX) -v
	echo $(RUNTIMR_SRCS_SECTION)
	echo $(RUNTIMR_TEST_SECTION)
	echo $(RUNTIME_HEADER_PATH)
	echo $(SRCS)
	echo $(OBJS)

.PHONY: test all clean

1.Makefile:remove the
