FROM circleci/python:2.7.18-node-browsers

ENV CIRCLE_ARTIFACTS=/tmp/circleci-artifacts
ENV CIRCLE_TEST_REPORTS=/tmp/circleci-test-results

RUN sudo apt-get update
RUN sudo apt-get install build-essential libssl-dev libffi-dev python-dev
RUN sudo apt-get install -y postgresql-client || true
RUN mkdir -p $CIRCLE_ARTIFACTS $CIRCLE_TEST_REPORTS
RUN sudo wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
RUN sudo chmod a+x lein
RUN sudo mv lein /usr/local/bin/lein
RUN pip install --user awscli==1.11.75
RUN pip install --user --upgrade pip setuptools wheel
RUN aws configure set default.region us-west-2
RUN sudo npm install -g bower
RUN sudo npm install -g less@3.10.3
RUN sudo npm install -g karma karma-chrome-launcher karma-cljs-test
RUN npm install
RUN git clone https://github.com/Homebrew/brew ~/.linuxbrew/Homebrew \
&& mkdir ~/.linuxbrew/bin \
&& ln -s ../Homebrew/bin/brew ~/.linuxbrew/bin \
&& eval $(~/.linuxbrew/bin/brew shellenv) \
&& brew tap aws/tap \
&& brew install aws-sam-cli
RUN mv ~/.linuxbrew/Cellar/aws-sam-cli/1.12.0.reinstall/ ~/.linuxbrew/Cellar/aws-sam-cli/1.12.0/
RUN mv ~/.linuxbrew/Cellar/python\@3.8/3.8.6_2.reinstall/ ~/.linuxbrew/Cellar/python\@3.8/3.8.6_2/
RUN echo 'export PATH="/home/circleci/.linuxbrew/opt/aws-sam-cli/bin:$PATH"' >> ~/.profile
ENV PATH="/home/circleci/.linuxbrew/opt/aws-sam-cli/bin:$PATH"
