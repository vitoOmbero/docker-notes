# build

```bash
cd flask-app
docker image build -t test-py-app .
```
## run

```bash
docker container run -d -p 8888:5000 test-py-app
```
