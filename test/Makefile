CXX = g++
CPPFLAGS += -I/usr/local/include -pthread
CXXFLAGS += -std=c++11 -g
LDFLAGS += -L/usr/local/lib `pkg-config --libs grpc++ grpc`       \
           -Wl,--no-as-needed -lgrpc++_reflection -Wl,--as-needed \
           -lprotobuf -lpthread -ldl

MAPREDUCE_LIB = -L../external/lib -lmapreduce
MR_WORKER_LIB = -L../external/lib -lmr_worker

all: mrdemo mr_worker

mrdemo: main.o
	$(CXX) $^ -o $@ $(LDFLAGS) $(MAPREDUCE_LIB) $(LDFLAGS)

mr_worker: user_tasks.o
	$(CXX) $^ -o $@ $(LDFLAGS) $(MR_WORKER_LIB) $(LDFLAGS)

%.o: %.cc
	$(CXX) -c $< -I../external/include $(CXXFLAGS)

clean:
	rm -rf *.o *.pb.cc *.pb.h mrdemo mr_worker ./output/*
