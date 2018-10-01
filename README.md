<p align="center"><a href="https://auklet.io"><img src="https://s3.amazonaws.com/auklet/static/auklet_python.png" alt="Auklet - Problem Solving Software for Python"></a></p>

# Auklet for Python
<a href="https://pypi.python.org/pypi/auklet" alt="PyPi page link -- version"><img src="https://img.shields.io/pypi/v/auklet.svg" /></a>
<a href="https://pypi.python.org/pypi/auklet" alt="PyPi page link -- Apache 2.0 License"><img src="https://img.shields.io/pypi/l/auklet.svg" /></a>
<a href="https://pypi.python.org/pypi/auklet" alt="Python Versions"><img src="https://img.shields.io/pypi/pyversions/auklet.svg" /></a>
<a href="https://codeclimate.com/repos/5a54e10be3d6cb4d7d0007a8/maintainability" alt="Code Climate Maintainability"><img src="https://api.codeclimate.com/v1/badges/7c2cd3bc63a70ac7fd73/maintainability" /></a>
<a href="https://codeclimate.com/repos/5a54e10be3d6cb4d7d0007a8/test_coverage" alt="Test Coverage"><img src="https://api.codeclimate.com/v1/badges/7c2cd3bc63a70ac7fd73/test_coverage" /></a>

This is the official Python agent for [Auklet][brochure_site]. It officialy supports Python 2.7.9+ and 3.4-3.7, and runs on most POSIX-based operating systems (Debian, Ubuntu Core, Raspbian, QNX, etc).

## Features
- Automatic report of unhandled exceptions
- Automatic Function performance issue reporting
- Location, system architecture, and system metrics identification for all issues
- Ability to define data usage restriction


## Compliance
Auklet is an edge first application performance monitor; therefore, starting with version 1.0.0 we maintain the following compliance levels:

- Automotive Safety Integrity Level B (ASIL B)

If there are additional compliances that your industry requires please contact the team at <hello@auklet.io>.

## Quickstart
To install the agent with _pip_:

```bash
pip install auklet
```

To setup Auklet monitoring in your application:

```python
from auklet.monitoring import Monitoring
auklet_monitoring = Monitoring(
    api_key="<API_KEY>",
    app_id="<APP_ID>",
    release="<CURRENT_COMMIT_HASH>"
)
auklet_monitoring.start()
# Call your main function
main()
auklet_monitoring.stop()
```

### Authorization
To authorize your application you need to provide both an API key and app ID. These values are available in the connection settings of your application as well as during initial setup.

### Release Tracking
To track releases and identify which devices are running which version of code, we currently require that you provide the Git commit hash of your deployed code. This value needs to be passed into the constructor through `release`. The value needs to be the commit hash that represents the deployed version of your application. There are a few different ways you can do this, based upon how you choose to deploy your application.

#### Get Release via Subprocess
If you package and deploy your entire Git repository (including the `.git` directory), and if you have `git` installed on your devices, you can get the commit hash via a subprocess:

```python
git_commit_hash = subprocess.check_output(['git', 'rev-parse', 'HEAD'])
                  .decode('utf8').strip('\n')
```

#### Get Release via Environment Variable
If you package your app and deploy it without access to `git`, you can pass the commit hash to your app using the environment variable `APPLICATION_GIT_COMMIT_HASH`:

```python
git_commit_hash = os.environ.get("APPLICATION_GIT_COMMIT_HASH")
```

#### Get Release via File
Lastly, if it is difficult or impossible to set an environment variable via your deployment platform, you can include a new file in your packaged deployment which contains the commit hash. You can read from this file and supply the value to the constructor.

At packaging time, write the commit hash to a file and then include it in your package:

```bash
git rev-parse HEAD > path/to/git_commit_hash.txt
```

At runtime, read the included file as follows:

```python
release_file = open("git_commit_hash.txt", "r")
git_commit_hash = release_file.read().decode('utf8').strip('\n')
```

#### Define Your Own Version
You can also provide your own version string in the constructor:

```python
from auklet.monitoring import Monitoring
auklet_monitoring = Monitoring(
    api_key="<API_KEY>",
    app_id="<APP_ID>",
    release="<CURRENT_COMMIT_HASH>",
    version="<DEFINED_VERSION>"
)
```

## Resources
- [Auklet][brochure_site]
- [Python Documentation](https://docs.auklet.io/docs/python-integration)
- [Issue Tracker](https://github.com/aukletio/Auklet-Agent-Python/issues)

[brochure_site]: https://auklet.io
