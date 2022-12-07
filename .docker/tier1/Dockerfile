FROM dmoj/runtimes-tier1
ARG TAG=master
ADD problems /mnt/problems

RUN mkdir /judge && cd /judge && \
	curl -L https://github.com/DMOJ/judge-server/archive/"${TAG}".tar.gz | tar -xz --strip-components=1 && \
	pip3 install -e . && \
	python3 setup.py develop && \
	HOME=~judge . ~judge/.profile && \
	runuser -u judge -w PATH -- dmoj-autoconf -V > /judge-runtime-paths.yml && \
	echo '  crt_x86_in_lib32: true' >> /judge-runtime-paths.yml

ENTRYPOINT runuser -u judge -w PATH -- dmoj -c /problems/judge_conf.yml 192.168.0.100

ENTRYPOINT ["/judge/.docker/entry"]
