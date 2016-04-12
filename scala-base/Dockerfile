
FROM java:jre

ENV scala_version=2.11.8
ENV scala_deb_url=http://www.scala-lang.org/files/archive/scala-$scala_version.deb

RUN depsRuntime=' \
	' \
  && depsBuild=' \
		curl \
	' \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends $depsRuntime \
	&& apt-get install -y --no-install-recommends $depsBuild \
  && curl -SL "$scala_deb_url" -o scala.deb \
	&& dpkg -i scala.deb \
	&& rm scala.deb \
	&& apt-get purge -y --auto-remove $depsBuild \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*
