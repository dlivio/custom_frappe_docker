ARG FRAPPE_BRANCH=develop
FROM frappe/erpnext-worker:${FRAPPE_BRANCH}

RUN install_app project_extension https://github.com/dlivio/project_extension master && \
  install_app bench_manager https://github.com/frappe/bench_manager develop