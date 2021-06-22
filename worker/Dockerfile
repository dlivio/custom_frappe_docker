ARG FRAPPE_BRANCH=develop
FROM frappe/erpnext-worker:${FRAPPE_BRANCH}

RUN install_app ipcameras https://github.com/dlivio/ipcameras master && \
  install_app bench_manager https://github.com/frappe/bench_manager develop
