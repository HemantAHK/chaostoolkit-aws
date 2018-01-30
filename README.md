# Chaos Toolkit Extension for AWS

[![Build Status](https://travis-ci.org/chaostoolkit-incubator/chaostoolkit-aws.svg?branch=master)](https://travis-ci.org/chaostoolkit-incubator/chaostoolkit-aws)
[![Python versions](https://img.shields.io/pypi/pyversions/chaostoolkit-aws.svg)](https://www.python.org/)

This project is a collection of [actions][] and [probes][], gathered as an
extension to the [Chaos Toolkit][chaostoolkit].

[actions]: http://chaostoolkit.org/reference/api/experiment/#action
[probes]: http://chaostoolkit.org/reference/api/experiment/#probe
[chaostoolkit]: http://chaostoolkit.org

## Install

This package requires Python 3.5+

To be used from your experiment, this package must be installed in the Python
environment where [chaostoolkit][] already lives.

```
$ pip install -U chaostoolkit-aws
```

## Usage

To use the probes and actions from this package, add the following to your
experiment file:

```json
{
    "name": "stop-an-ec2-instance",
    "provider": {
        "type": "python",
        "module": "chaosaws.ec2.actions",
        "func": "stop_instance",
        "arguments": {
            "instance_id": "i-123456"
        }
    }
}
```

That's it!

Please explore the code to see existing probes and actions.

## Configuration

This extension uses the [boto3][] library under the hood. This library expects
that you have properly [configured][creds] your environment to connect and
authenticate with the AWS services.

[boto3]: https://boto3.readthedocs.io
[creds]: https://boto3.readthedocs.io/en/latest/guide/configuration.html

Generally speaking, there are two ways of doing this:

* you have [configured][creds] the environment where you will run the
  experiment from (so either with a `~/.aws/credentials` or proper environment
  variables)
* you explicitely pass the correct environment variables to the experiment
  definition as follows:

    ```json
    {
        "secrets": {
            "aws": {
                "aws_access_key_id": "your key",
                "aws_secret_access_key": "access key",
                "aws_session_token": "token",
            }
        }
    }
    ```

  Note that the token is optional.

## Test

To run the tests for the project execute the following:

```
$ pytest
```

## Contribute

If you wish to contribute more functions to this package, you are more than
welcome to do so. Please, fork this project, make your changes following the
usual [PEP 8][pep8] code style, sprinkling with tests and submit a PR for
review.

[pep8]: https://pycodestyle.readthedocs.io/en/latest/

The Chaos Toolkit projects require all contributors must sign a
[Developer Certificate of Origin][dco] on each commit they would like to merge
into the master branch of the repository. Please, make sure you can abide by
the rules of the DCO before submitting a PR.

[dco]: https://github.com/probot/dco#how-it-works