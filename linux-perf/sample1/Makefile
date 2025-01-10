FLAMEGRAPH=/home/ssc/src/FlameGraph

all: clean

compile: clean
	clang sample.c -g -o sample

stat: compile
	sudo perf stat ./sample 2000

profile: compile
	sudo perf record -F 999 ./sample 2000
	sudo chmod 777 perf.data
	perf report

top: clean
	sudo perf record -F 99 -a -g -- sleep 5
	sudo chmod 777 perf.data
	perf script | ${FLAMEGRAPH}/stackcollapse-perf.pl > out.folded
	${FLAMEGRAPH}/flamegraph.pl out.folded > perf.svg

clean:
	rm -f *.perf *.unfolded *.folded perf.data *.old *.svg sample *.out
	clear
