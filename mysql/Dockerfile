# =============================================================================
#
# MYSQL 5.7
# 
# =============================================================================
FROM mysql:5.7

LABEL maintainer="henry@cajanegra.com.ec"

# -----------------------------------------------------------------------------
# Additional repositories
# -----------------------------------------------------------------------------
RUN apt-get update -y && \
    apt-get install -y \
    curl ethtool hostname tar unzip vim wget htop

# -----------------------------------------------------------------------------
# Import Database and configuration
# -----------------------------------------------------------------------------
ADD databases/leadsgenerator.sql.gz /docker-entrypoint-initdb.d
COPY config/mysqld.cnf /etc/mysql/mysql.conf.d/mysqld.cnf