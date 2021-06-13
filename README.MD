Collection of edited notebooks from Underactuated Robotics: https://github.com/RussTedrake/underactuated

### Using Google Colabs

Add this code snippet to any .ipynb notebook in order to run drake within Colabs:

```
import importlib
import sys
from urllib.request import urlretrieve

# Install drake (and underactuated).
if 'google.colab' in sys.modules and importlib.util.find_spec('underactuated') is None:
    urlretrieve(f"http://underactuated.csail.mit.edu/scripts/setup/setup_underactuated_colab.py",
                "setup_underactuated_colab.py")
    from setup_underactuated_colab import setup_underactuated
    setup_underactuated(underactuated_sha='560c2adace05eb20ebd78377582015d5b2d3859a', drake_version='0.25.0', drake_build='releases')

server_args = []
if 'google.colab' in sys.modules:
  server_args = ['--ngrok_http_tunnel']
# Start a single meshcat server instance to use for the remainder of this notebook.
from meshcat.servers.zmqserver import start_zmq_server_as_subprocess
proc, zmq_url, web_url = start_zmq_server_as_subprocess(server_args=server_args)
```

### Using Docker

Pull the docker image from https://hub.docker.com/r/russtedrake/underactuated with this command from your terminal:

```
docker pull russtedrake/underactuated
```

Run a docker container with the pulled image via:
```
docker run -i -t russtedrake/underactuated /bin/bash
```

