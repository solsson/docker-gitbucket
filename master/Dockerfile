
FROM solsson/gitbucket:scala-build

ENV gitbucket_source=https://github.com/gitbucket/gitbucket/archive/master.tar.gz

RUN depsRuntime=' \
	' \
  && depsBuild=' \
		curl \
	' \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends $depsRuntime \
	&& apt-get install -y --no-install-recommends $depsBuild \
  && curl -SLs "$gitbucket_source" -o ~/gitbucket.tar.gz \
  && cd / \
	&& mkdir -p src \
	&& tar xzf ~/gitbucket.tar.gz -C src --strip-components=1 \
	&& rm ~/gitbucket.tar.gz \
  && cd src \
  && sbt package \
  && find target -name "gitbucket*.war" -exec mv -v '{}' /opt/gitbucket.war \; \
	&& apt-get purge -y --auto-remove $depsBuild \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

# The rest is a copy of `latest` dockerfile

RUN ln -s /gitbucket /root/.gitbucket

VOLUME /gitbucket

# Port for web page
EXPOSE 8080
# Port for SSH access to git repository (Optional)
EXPOSE 29418

CMD ["java", "-jar", "/opt/gitbucket.war"]
