# Debian VPS: Which Release to Run, How Much RAM Your Stack Needs, and When Managed Support Is Worth Paying For (With a Full Plan Comparison)

New Debian servers should be built on Debian 13 (Trixie). Debian 12 Bookworm left full security support in June 2026 and now runs on LTS fixes through 2028, which makes it a compatibility pick rather than a starting point. The plan decision matters more than the release for most buyers: 2 GB runs one Nginx site and a small database, while 4 GB is roughly where containers and a real database stop competing for the same memory.

> **Quick pick:** for a public site, an API, or anything answering on port 443, SixtyNet's LAX-STARTER (2 vCPU, 2 GB RAM, 40 GB NVMe, 5 TB traffic, DDoS protection) is **$200/year** at the current annual rate, down from $240. For scraping, social account work, or any job that needs a residential IP, the residential line starts at **$260/year**, and ports 80 and 443 stay closed on those plans.
>
> 👉 [See SixtyNet's VPS plans and current annual rates](https://sixtynet.net/aff.php?aff=39)

## Pick the Debian release before you pick the box

| Release | Where it stands | Kernel | What it means for a new server |
| --- | --- | --- | --- |
| Debian 13 "Trixie" | Current stable since August 2025 | 6.12 | Default choice; roughly 3 years of full security support, then LTS |
| Debian 12 "Bookworm" | Full support ended June 2026 | 6.1 | Now on LTS security fixes until June 2028; use it for legacy compatibility |
| Debian 11 "Bullseye" | LTS only | — | Only when an application pins you to it |

Debian gives each stable release about three years of full security support plus two more years from the LTS team, so a version you install today has a five-year window before you have to think about it again. Package versions inside that window barely move. Debian freezes a release for months before shipping it and vets updates carefully, which is why a Bookworm box from last year still runs the software you tested against it. It also ships more than 51,000 packages through APT, so the libraries your application needs are usually one `apt install` away.

The caveat for 2026 buyers is that provider panels lag the release. A UK host's configurator still listed only Bookworm in September 2026, more than a year after Trixie became stable, and that is not unusual. Check the OS template list before you pay rather than after.

👉 [Open SixtyNet's VPS page and check the OS templates on offer](https://sixtynet.net/aff.php?aff=39)

Bulletproof, upgrade later: if you end up on Bookworm because a template forces it, the in-place move to Trixie is the standard Debian path. Back up first, then `apt update`, `apt full-upgrade`, and reboot, following the release notes. Allow an hour and read the notes for the packages you actually run.

## What SixtyNet sells, plan by plan

SixtyNet runs two product lines on AMD EPYC hardware with NVMe storage: instances that come with a residential IP attached, and DDoS-protected plans named for Los Angeles. Both lines carry a premium network, and the residential line is the specialist product here.

Annual billing is where the discount sits. These are the plans with published annual rates:

| Plan | vCPU / RAM / NVMe | Network and traffic | Annual rate | Order |
| --- | --- | --- | --- | --- |
| Residential-STARTER | 2 / 2 GB / 40 GB | 2G premium, 5 TB | **$260** (from $300) | [Order](https://sixtynet.net/aff.php?aff=39) |
| LAX-STARTER | 2 / 2 GB / 40 GB | 2G premium, 5 TB, DDoS | **$200** (from $240) | [Order](https://sixtynet.net/aff.php?aff=39) |
| LAX-MICRO | 4 / 4 GB / 80 GB | 4G premium, 10 TB, DDoS | **$400** (from $480) | [Order](https://sixtynet.net/aff.php?aff=39) |
| LAX-LARGE | 8 / 16 GB / 320 GB | 10G premium, 40 TB, DDoS | **$1,600** (from $1,920) | [Order](https://sixtynet.net/aff.php?aff=39) |

The four above work out to roughly $16.67, $21.67, $33.33 and $133 a month if you amortise the annual figure. The page also lists quarterly billing and a smaller quarterly discount, so annual is the cheapest cadence rather than the only one.

The remaining tiers on the same page are larger residential instances, China-optimised residential instances, and a storage-focused plan. Rates for these are shown on the plan page:

| Tier | vCPU / RAM / NVMe | Network and traffic | Notes |
| --- | --- | --- | --- |
| Residential, tier 2 | 4 / 4 GB / 80 GB | 4G premium, 10 TB | Residential IP, ports 80/443 closed |
| Residential, tier 3 | 8 / 8 GB / 160 GB | 10G premium, 20 TB | Same restrictions |
| Residential, tier 4 | 16 / 16 GB / 320 GB | 10G premium, 40 TB | Same restrictions |
| China-optimised residential | 2 / 2 GB / 40 GB | 2G premium, 5 TB | AS9929 routing, rejects external scans |
| China-optimised residential | 4 / 4 GB / 80 GB | 4G premium, 10 TB | Same restrictions |
| Storage plan | 4 / 4 GB / 300 GB + 200 GB bonus RAID 10 | 10G premium, 10 TB | DDoS protection |

Two network details on that page are worth understanding before you compare prices. Disk throughput is published per plan, at 12,500 IOPS on the smaller instances and 25,000 on the larger ones, which is a more honest number to compare than "NVMe" on its own. The page also lists a 100 Mbps base network with a 3× burst and 95th-percentile billing, plus free BGP session setup. Ninety-fifth-percentile billing means short spikes are discarded before you are charged, so a burst of traffic during a deploy does not become an overage.

## Debian or Ubuntu on the same box?

Both use APT, dpkg, and systemd, and the commands in your runbook barely change between them. The difference is cadence. Ubuntu ships new packages faster, has a fixed LTS rhythm and commercial backing behind it, and most tutorials you will find online assume it. Debian moves slower on purpose and asks you to work within the versions it froze.

For a production server that runs one application stack and gets rebuilt rarely, Debian's conservatism is the useful part. For a team that wants the newest PHP or Node without adding a repository, Ubuntu saves a step. Neither is the wrong answer, and picking Debian because it is "more stable" without checking whether your framework needs a newer library is how people end up compiling things from source on a Sunday.

## Self-managed or managed: where the line actually falls

SixtyNet's plan list does not include a managed tier, so treat these instances as self-managed and read the table below as your actual job description.

| Task | Self-managed | Managed |
| --- | --- | --- |
| Root access | You | You |
| Debian installation | Included | Included |
| OS updates | You | Provider |
| Security hardening | You | Provider, within the supported scope |
| Application administration | You | **Still you** |
| Monitoring | Basic infrastructure only | Provider, often 24/7 |
| Backups | Depends on what you bought | Depends on the plan |

Application management staying with you in both models is the part buyers miss. A managed plan covers the operating system underneath, not the WordPress plugin, the database schema, or the reason your queue worker died at 3 a.m. Backups are the other variable: one provider we reviewed includes them in the managed service, another treats them as an add-on at every tier. Read the specific plan.

The decision rule is unglamorous. If someone on your side reads logs and can be woken up to patch a box, self-managed is cheaper and gives you full control. If nobody owns that, a managed plan removes the OS-update chore but still leaves you the application. Budget for the fact that you are buying the smaller half of the work.

## What the price gap between two "2 core 4 GB" plans pays for

Entry-level 2 GB KVM instances from mainstream US hosts sit around $5 to $8 a month. SixtyNet's LAX-STARTER is about $16.67 a month on annual billing, so the premium is real and it is not buying raw CPU. What it buys is network and IP type: premium routing, DDoS protection and, on the residential line, an address that does not belong to a datacenter range.

That premium is the point if your workload needs those things, and wasted money if it does not. A Debian box serving a brochure site to US and European visitors gains nothing from China-optimised routing.

Some concrete things to check when comparing any two quotes at the same spec, because they explain most of the price difference:

- **Virtualisation.** KVM full virtualisation is the baseline. Anything advertising OpenVZ or a "container VPS" gives you less isolation and a kernel you cannot change.
- **Storage redundancy.** Some hosts keep three copies of your data across a Ceph cluster so a failed node does not take your disk with it. SixtyNet's storage plan specifies RAID 10.
- **Backups, default or add-on.** A $6 plan with $3 backups is not cheaper than an $8 plan that includes them. Check whether snapshots are self-service and restorable from the panel.
- **Rebuild and rescue.** Reinstalling an OS should take under a minute or two on modern infrastructure, and a rescue mode that mounts your disk as root is the difference between a 20-minute fix and a lost night.
- **API and automation.** If you manage more than a couple of servers, an API that covers redeploys, snapshots and firewall rules matters more than 500 MHz of CPU.
- **Published benchmarks.** Treat a provider's benchmark page as marketing about one specific test machine, not a promise about the plan you buy. Look at IOPS, network and CPU figures, then discount them for your own workload.

👉 [Compare SixtyNet's plan specs and per-plan IOPS figures](https://sixtynet.net/aff.php?aff=39)

## The two residential restrictions that decide the purchase

The residential plans do not open ports 80 and 443, because the IP risk controls that make them useful also block public web serving. If your project starts with "install Nginx and point a domain at it," a residential plan is the wrong product and no amount of configuration will fix it. The LAX plans exist for that use case.

Refunds on the China-optimised residential instances are issued as account balance rather than back to your payment method, which changes the maths if you are trialling the service. Both of these are on the product page rather than buried in a policy document, and both are easy to miss when you are comparing core counts.

On location, third-party write-ups describe a single Los Angeles facility with expansion planned. If your audience or compliance requirements point at Europe or Asia, ask before ordering rather than assume.

## A security baseline for a fresh Debian box

Debian's minimal default install is a starting point, not a hardened server. In any case, an image can arrive without `unattended-upgrades` configured, so you are the update mechanism until you set one up.

1. Add SSH keys for every user and turn off password authentication.
2. Set up a firewall and allow only the ports the application needs.
3. Disable services you are not using; fewer listening sockets means a smaller attack surface.
4. Stop logging in as root and give each person their own account with sudo.
5. Configure automatic security updates, then verify they actually ran after a week.
6. Back up off the server, not just to a snapshot on the same host.
7. Watch CPU, memory, disk, logs and uptime so you find out before your users do.

Application and database configuration is where most real incidents start. Debian can only give you a stable base.

## FAQ

**Is Debian 12 still safe for a new server?**
It receives LTS security fixes until June 2028, so a short-lived project is fine on it. New builds should use Debian 13 to get the full support window rather than starting two years into an ageing one.

**How much RAM does a Debian VPS need?**
1 GB runs a minimal install and a lightweight service. 2 GB is comfortable for a single site with a small database. Move to 4 GB once you add containers, a real database workload, or several background workers.

**Can I host a public website on a residential IP VPS?**
Not on SixtyNet's residential line, since ports 80 and 443 are closed. Use the LAX plans for anything that needs to accept HTTP traffic.

## Which plan to order

- One site, a small database, public traffic → **LAX-STARTER at $200/year**. Two cores and 2 GB is enough for a Debian box running Nginx and MariaDB if traffic stays modest.
- Containers, PostgreSQL, background workers → **LAX-MICRO at $400/year**. The extra 2 GB and 40 GB of disk are the difference between a box that swaps under load and one that does not.
- Scraping, account management, anything that needs a residential IP → **Residential-STARTER at $260/year**, with no expectation of public web serving.
- Data that has to survive a node failure → the storage plan's RAID 10, plus your own off-site backups.

Two things to confirm before you pay: that the panel lists Debian 13 among its templates, and the renewal rate for the second year, since the annual figures above are discounted from a higher list price. Then you can configure the box once and leave it alone.

👉 [Start with SixtyNet's LAX-STARTER at the current annual rate](https://sixtynet.net/aff.php?aff=39)
