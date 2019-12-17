FROM electronuserland/builder:wine

# Create user "jenkins"
RUN id jenkins 2>/dev/null || useradd --uid 1000 --create-home jenkins
RUN cp -a /root/.wine /home/jenkins/ && chown -R jenkins /home/jenkins/.wine

# EOF
