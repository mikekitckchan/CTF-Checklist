## Introduction

This is a note taking from talk of TomNomNom from NahamSec's Live Recon Series. This talk is about how to create a customized wordlist for a target.

#### Steps

- Use GAU, Burp, webpaste or any other tools to capture as much endpoint as possible

- Use unfrl to extract the endpoints info

- Use ```sed 's#/#\n#g' paths.txt | sort -u``` to extract each elements of the endpoints.

