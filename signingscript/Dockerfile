FROM escapewindow/nix:latest
MAINTAINER Mozilla Releng release+nix@mozilla.com

RUN su -l -c "nix-env -iA nixpkgs.git" nixbld
RUN su -l -c "cd && git clone https://github.com/escapewindow/signingscript.git && cd signingscript && git checkout nix" nixbld
RUN su -l -c "cd && nix-build signingscript/release.nix -A docker" nixbld
