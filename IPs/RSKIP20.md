# Survive and Ephemeral Memory Spaces

|RSKIP          |20           |
| :------------ |:-------------|
|**Title**      |Survive and Ephemeral Memory Spaces |
|**Created**    |25-NOV-16 |
|**Author**     |SDL |
|**Purpose**    |Sca |
|**Layer**      |Core |
|**Complexity** |2 |
|**Status**     |Draft |

## Pre-git revisions

Date: 25/NOV/2016

Revision date: 

Revision: 1

Status: Draft (unfinished)

## Abstract

This RSKIP splits the storage memory into two subspaces: survive and ephemeral. The first is hibernated, but the second is destroyed on hibernation.
Motivation

This, combined with contract rent, allows a un-owned or public contract to choose which parts of the memory will persist will very low overhead and high efficiency if some clients of the contract do not pay the rent.

## Specification
TBD

## Sample Use Cases

### User-asset contract

A contract ASSET maintains a local ledger in (a,v) pairs, such that “a“ is the address of the asset owner and “v“ is the asset value owned. When a receives an asset for the first time, a transfer() method is called, and a new memory cell is created in the survive subspace. The user will periodically (once every 6 months) call a method payRent() of the ASSET contract. The method will check if the address is in the survive subspace, and if not, it will move the address there, and pay a deposit corresponding to the cost of 6 months of storage.

```
public payRent()
{
    address a = msg.sender;
    Amount amount = GASCOST(memoryCost)*2;
    rentPaid[a] = block.date	
    DEPOSIT_RENT(this,amount)
}

```
