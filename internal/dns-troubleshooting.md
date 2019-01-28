# DNS Troubleshooting

If you are seeing infrequent ssl or dns issues, nginx is a good place to start troubleshooting.

Log in and check the error log:

`tail -f /var/log/nginx/error.frontend.opencollective.log`

When we switched to v2 frontend, we had to increase workers and file limits for nginx: [https://stackoverflow.com/a/36500262](https://stackoverflow.com/a/36500262). On 10/26/2017, I changed it from 768 to 2000.

Once we increased worker limit, we hit open file limit: [https://www.cyberciti.biz/faq/linux-unix-nginx-too-many-open-files/](https://www.cyberciti.biz/faq/linux-unix-nginx-too-many-open-files/). On 10/26/2017, I added a limit of 70000 files and added nginx hard and soft limits to 30000 and 10000, respectively.

Once we made this change, all urls in nginx config for opencollective domain were changed to https \(except image server, which is still http\).

