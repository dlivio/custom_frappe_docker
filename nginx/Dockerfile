ARG FRAPPE_BRANCH=develop
FROM node:14-buster
ARG FRAPPE_BRANCH=develop

RUN apt-get update && apt-get install -y git

COPY install_frappe.sh /install_frappe
COPY install_erpnext.sh /install_erpnext
COPY install_app.sh /install_app
COPY prepare_production.sh /prepare_production

# Install frappe
RUN /install_frappe ${FRAPPE_BRANCH} && \
  # Install erpnext
  /install_erpnext && \
  # Install required apps with following command
  # /install_app ipcameras https://github.com/dlivio/ipcameras master && \
  /install_app project_extension https://github.com/dlivio/project_extension.git master && \
  # /install_app posawesome https://github.com/yrestom/POS-Awesome master && \
  # /install_app frappe_s3_attachment https://github.com/zerodha/frappe-attachments-s3 master && \
  # /install_app metabase_integration https://github.com/pipech/frappe-metabase master && \
  # /install_app bookings https://github.com/franknyarkoh/bookings master && \
  /install_app bench_manager https://github.com/frappe/bench_manager develop && \
  # Cleanup for production
  /prepare_production

FROM frappe/erpnext-nginx:${FRAPPE_BRANCH}

COPY --from=0 /home/frappe/frappe-bench/sites/ /var/www/html/
COPY --from=0 /rsync /rsync

# Append list of installed to apps.txt
RUN echo -n "posawesome\nfrappe_s3_attachment\nmetabase_integration\nbookings\nbench_manager" >> /var/www/html/apps.txt

VOLUME [ "/assets" ]

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]
