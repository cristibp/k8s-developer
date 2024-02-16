POD_NAME=webapp-xyz-abc
LOCAL_PORT=39001
oc port-forward pod/$POD_NAME ${LOCAL_PORT}:8000 &


POD_NAME=webapp-6c66d49786-7wjwv
LOCAL_PORT=39001
oc port-forward pod/$POD_NAME ${LOCAL_PORT}:8000 &