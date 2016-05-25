============================
ONI User Feedback Data Flow
============================

In the operational analytics component, the user may rate the connections found by ONI based upon how suspicious the connection appears to the user.
This information is then forwareded to the oni-ml component to guide suspicion calculations, so that connections judged non-suspicious are less likely to be flagged suspicious in the
future.

This design document describes how data is communicated from the OA component back to the ML component.

Prerequisites
=============
To allow the flow_scores.csv file to be correctly copied to the LPATH, there needs to be an ssh key created on the OA node and copied to the ML node; this, to enable unattended and secure file transfer between nodes.

Data Location
=============

The ML component expects that the file flow_scores.csv be placed by the OA component in the directory LPATH, as defined in the ONI configuration file.

Requirements on the ML Cleanup Routines
---------------------------------------
Because the flow_scores.csv file is expected to be in the LPATH directory, the LPATH directory cannot be "blown away" prior to running ML.


Data Format
===========

The ML component expects that the feed back data provided by the OA component be a comma-separated text file adhering to the following schema:


sev,tstart,srcIP,dstIP,sport,dport,proto,flag,ipkt,ibyt,lda_score,rank,srcIpInternal,destIpInternal,srcGeo,dstGeo,srcDomain,dstDomain,gtiSrcRep,gtiDstRep,norseSrcRep,norseDstRep
