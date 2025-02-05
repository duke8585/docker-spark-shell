FROM apache/spark:3.5.4-scala2.12-java11-python3-r-ubuntu

# Switch to root for package installation
USER root

# Install rlwrap for better shell experience # NOTE seems optional
# RUN apt-get update && \
#     apt-get install -y rlwrap && \
#     rm -rf /var/lib/apt/lists/*

# Add Spark binaries to the PATH
ENV SPARK_HOME=/opt/spark
ENV PATH="$SPARK_HOME/bin:$SPARK_HOME/sbin:$PATH"

# Fix missing home directory issue
RUN mkdir -p /home/spark && \
    chown -R 185:185 /home/spark

# Ensure correct HOME directory
ENV HOME=/home/spark

# Enable proper JLine handling for spark-shell
RUN mkdir -p /home/spark/.jline && \
    echo "set editing-mode vi" > /home/spark/.jline/inputrc && \
    echo "set completion-ignore-case on" >> /home/spark/.jline/inputrc && \
    echo "set show-all-if-ambiguous on" >> /home/spark/.jline/inputrc && \
    echo "TAB: menu-complete" >> /home/spark/.jline/inputrc && \
    chown -R 185:185 /home/spark/.jline

# Switch back to Spark’s default user (UID 185)
USER 185

# Set default entrypoint to bash
CMD ["/bin/bash", "-l", "-c", "export INPUTRC=/home/spark/.jline/inputrc && exec bash"]