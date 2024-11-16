
```sh
# Install and Use pyenv
curl https://pyenv.run | bash


# Add pyenv to Your Shell: Add the following lines to your shell’s configuration file (~/.bashrc, ~/.zshrc, or similar):
sudo vi ~/.bashrc

# copy and paste
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"

# Then, restart your shell or source the config file:
source ~/.bashrc  # or ~/.zshrc, etc.


# Install SQLite and Other Required Packages
sudo apt update
sudo apt install -y libsqlite3-dev libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libffi-dev liblzma-dev libncurses5-dev \
    libgdbm-dev libnss3-dev libtk8.6 libgmp-dev \
    build-essential
```

## Option 2: Manually Rebuild Python with Updated SQLite
If pyenv installation isn’t an option, you can manually rebuild Python from source, ensuring it links to the updated SQLite:

Ensure SQLite 3.45.3 is Installed and in the Right Path: Ensure that SQLite 3.45.3 is installed under /usr/local or a similar path accessible by Python.

```sh
# Rebuild Python 3.12.1 with Correct SQLite Linkage: 
wget https://www.python.org/ftp/python/3.12.1/Python-3.12.1.tgz
tar -xzf Python-3.12.1.tgz
cd Python-3.12.1
./configure --enable-optimizations --with-sqlite3=/usr/local  # Adjust path if needed
make
sudo make altinstall  # Installs as `python3.12`


# Recreate the Virtual Environment:
deactivate  # Exit if in a virtual environment
rm -rf _venv
python3.12 -m venv _venv  # Use the newly built Python version
source _venv/bin/activate
pip install -r requirements.txt
```


