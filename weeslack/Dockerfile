# Usage:
# 	Building
# 		docker build -t wee-slack .
#	Running (no saved state)
# 		docker run -it \
#			-v /etc/localtime:/etc/localtime:ro \ # for your time
# 			wee-slack
# 	Running (saved state)
# 		docker run -it \
#			-v /etc/localtime:/etc/localtime:ro \ # for your time
# 			-v "${HOME}/.weechat:/home/user/.weechat" \
# 			wee-slack
#
FROM fedora:latest

RUN /bin/dnf install -yq deltarpm 
RUN dnf install -yq git \
		    weechat \
                    python \
                    python2-lxml && \
    dnf clean all


RUN pip install websocket-client

RUN pip install pync

ENV HOME /home/user

ADD https://raw.githubusercontent.com/rawdigits/wee-slack/master/wee_slack.py /home/user/.weechat/python/autoload/wee_slack.py

RUN useradd  user -d $HOME \
	&& chown -R user $HOME

WORKDIR $HOME
USER user

ENTRYPOINT [ "weechat" ]

