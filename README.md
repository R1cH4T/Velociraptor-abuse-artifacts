# Velociraptor Abuse Detection Artifacts

Artifacts for identifying potentially unauthorized Velociraptor binaries on Windows systems.  
These detections help surface attacker-dropped executables, renamed agent binaries, or unsigned builds that may indicate misuse of Velociraptor during an intrusion.

## Background

In recent months, several public security reports and incident write-ups have described cases where Velociraptor — a legitimate DFIR platform — was repurposed by adversaries.  
Threat actors have been observed:

- deploying modified or unsigned Velociraptor builds  
- using renamed binaries for stealthy remote access  
- dropping agent executables across workstations and servers  
- leveraging Velociraptor capabilities for collection, lateral movement, and persistence  

Since these binaries can easily blend in with legitimate tools, just finding a file on disk isn’t enough.  
These artifacts aim to help defenders reliably spot suspicious Velociraptor-like binaries and quickly determine whether they are legitimate signed builds or manipulated executables.

## What this is for

Velociraptor is widely used by blue teams and IR practitioners — but the same features that make it powerful also make it attractive to attackers.  
These artifacts are meant to detect:

- cloned or malicious Velociraptor binaries  
- unsigned, self-signed, or modified executables  
- unexpected agent deployments anywhere in the environment  
- binaries left behind after unauthorized activity  

They’re lightweight, transparent, and easy to extend or integrate into automated collection workflows.

## Artifacts

The repository is organized as follows:

artifacts/
- Windows.Detection.VelociraptorAbuse.yaml
-  Windows.Detection.VelociraptorBinarySignature.yaml

examples/
- detections/


### Windows.Detection.VelociraptorAbuse

Scans common Windows volumes (C:, D:, F:, etc.) for binaries matching `*velo*.exe`.  
It automatically ignores:

- the official Velociraptor installation directory under `Program Files`  
- the local Velociraptor GUI filestore (`gui_datastore`)  

This reduces noise and highlights only unusual or unexpected binaries found on disk.

### Windows.Detection.VelociraptorBinarySignature

Performs an Authenticode signature check on discovered binaries and uploads them for review.  
Useful for confirming whether a file is:

- signed by Rapid7  
- unsigned or signed with an invalid/unknown certificate  
- tampered with or modified  
- built from untrusted or unknown sources  

## Usage

1. Import the YAML artifacts into your Velociraptor server.  
2. Run them on a single host or across multiple hosts.  
3. Review the output for unexpected Velociraptor-like binaries.  
4. Check signature details or file uploads to confirm whether the binary is legitimate.  
5. Investigate anything that doesn’t match what you expect in your environment.

## Related Work & References

These artifacts align with recent public research into Velociraptor misuse:

- **Velociraptor Advisory (CVE-2025-6264)**  
- **Rapid7 – Identifying and Mitigating Potential Velociraptor Abuse**  
- **Huntress – Velociraptor Misuse (Part 1 & 2)**  
- **Una al Día – Reutilización maliciosa de Velociraptor**  
- **Sophos – Velociraptor Incident Response Tool Abused for Remote Access**

The goal is simply to give defenders a practical starting point when hunting for potentially malicious Velociraptor binaries.

## License

This project is released under the MIT license.

