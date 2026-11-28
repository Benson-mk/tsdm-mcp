# What `tsdm-sdk` v0.1.1 verifies for paid resources

For [MCP #5](https://github.com/Benson-mk/tsdm-mcp/issues/5), the [published release][release] supports buying a **thread** headlessly and confirming a **download credit charge** headlessly. Buying a **seller-priced attachment** stops at the native browser. These outcomes are not interchangeable.

Use the intended forum member and canonical HTTPS origin. The host owns credentials, fresh reads and manual redirects; change session `continuity` even on a new login as the same member. Keep forms, signed URLs and continuations private. A prepared form or credit offer belongs to its creating client and session, not merely to a resource ID. [Trade contract][trade-contract] · [Media contract][media-contract] · [Session checks][session]

### Paid thread: the receipt verifies the opening post

`createTradeClient(host).preparePaidThread(tid)` checks the lock and opening post. A recognized form identifies the thread/post, author, price, credit, author's proceeds and projected balance. The fixture quotes **5 fictional credits**, **4** to the author, **95** remaining. An unrecognized offer can hand off to the thread; insufficient funds can be refused. Only `confirmPaidThread(form, true)` dispatches the single POST. [Preparation][prepare] · [Offer and approval fixture][trade-fixture]

`purchased` requires `thread_pay_succeed` (or recognized native success) **and** a fresh same-session read of the exact, now-readable opening post. Rendered content can suffice without raw text. This verifies access, not a ledger balance, every post or attachment bytes. `already-accessible` means readable before submission, or `credits_buy_thread` followed by the same readback; neither proves a new debit. A native page without a prior lock cannot establish purchase just because the lock is absent. A lost reply, wrong post or inconclusive readback is `uncertain`: inspect access, do not replay the consumed form. [Confirmation][confirm] · [Prior access and readback fixtures][prior] · [Loss and wrong-post fixtures][uncertain] · [Native limits][native]

### `attachcredit`: the charge and the file are separate results

`createMediaClient(host).downloadAttachment(offeredURL)` stops at a matching credit redirect. `credit-required` exposes the attachment ID and optional thread ID, **not an amount, currency or balance**. After consent, `confirmAttachmentCredit(offer)` consumes the offer for one effectful GET. `credit-confirmed` requires a recognized message and one same-attachment `ck` continuation; it is not a balance check or a file. The [debit fixture][debit] reports **−1 天使币 after dispatch**, not a pre-charge quote. A lost or unrecognized charge response, including a missing matching continuation, is `unknown`: the charge may have happened; do not retry it. [Offer][offer] · [Confirmation and resume][resume]

`resumeAttachment` separately reads under the original session and stops on another charge demand. A qualifying forum response returns `delivered`: file bytes, content type and an optional filename. The charged SDK fixture ends at `external-handoff`, **not bytes**. A separate [loopback HTTP test][loopback] observed external bytes using a credentialless host GET, no forum referrer and manual redirects. A different SDK fixture compares exact bytes from an already accessible signed link; that proves current access, not how it was acquired. Denial or a partial file is not delivery. [Charged journey][charged] · [Direct bytes and denial][bytes] · [Attachment qualification][baseline]

### `attachpay`: the SDK verifies a destination, not a sale

An offered purchase URL, matching redirect or recognized unpaid notice yields `browser-handoff` (`reason: "purchase"`). For an attachment lookup the SDK checks `aid` and, when known, `tid`. The [sample listing][listing] shows **3 天使币** for attachment 37 in thread 1000; the SDK does not fetch that price or open the purchase form. The [handoff fixture][handoff] makes one download request and zero purchase requests. Review terms in the intended member's browser. The handoff proves no approval, debit, prior ownership, entitlement or delivery. [Routing][routing] · [Public contract][media-contract]

**If headless seller purchases are required:** the missing reusable work belongs in `tsdm-sdk`: read the buyer's exact attachment offer and terms, bind explicit one-shot confirmation to it, distinguish prior access/refusal/unknown, then independently recheck access to that attachment. Keep byte delivery separate. MCP can present consent and results; this is not a decision to add that feature or to substitute `attachcredit` for it. [SDK/host boundary][boundary]

**Evidence limit.** The v0.1.1 archive matches its [release manifest][manifest]. Its [qualification][qualification] reran paid-thread tests with controlled responses; attachment evidence was carried forward from the [v0.1.0 baseline][baseline]. The recorded live observation on November 27, 2026 was a **signed-out board → thread read only**. No live purchase, credit movement, restricted download or browser completion was verified here. [Guest receipt][guest]

[release]: https://github.com/Benson-mk/tsdm-sdk/releases/tag/v0.1.1
[manifest]: https://github.com/Benson-mk/tsdm-sdk/releases/download/v0.1.1/release.json
[trade-contract]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/docs/trades.md?plain=1#L1-L5
[media-contract]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/docs/media.md?plain=1#L3-L17
[session]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/src/forum-client/media/host.ts#L59-L103
[prepare]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/src/forum-client/trades/client.ts#L301-L379
[trade-fixture]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/tests/install/trades.mjs#L174-L201
[confirm]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/src/forum-client/trades/client.ts#L405-L462
[prior]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/tests/install/trades.mjs#L336-L377
[uncertain]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/tests/install/trades.mjs#L428-L461
[native]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/evidence/trades/README.md?plain=1#L47-L58
[offer]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/src/forum-client/media/retrieval.ts#L287-L306
[debit]: https://github.com/Carinoasd/tsdm_client/blob/02df67e39ded906def5b868e8f8311ba735b316c/test/data/attachment_download/credit_taken.html#L12-L15
[resume]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/src/forum-client/media/retrieval.ts#L358-L415
[charged]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/tests/install/media.mjs#L423-L473
[loopback]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/evidence/media/README.md?plain=1#L5-L11
[bytes]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/tests/install/media.mjs#L353-L390
[listing]: https://github.com/Carinoasd/tsdm_client/blob/02df67e39ded906def5b868e8f8311ba735b316c/test/data/attachment_download/post_attachments.html#L33-L49
[handoff]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/tests/install/media.mjs#L393-L421
[routing]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/src/forum-client/media/retrieval.ts#L263-L347
[boundary]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/docs/adr/0003-define-the-standalone-sdk-caller-contract.md?plain=1#L1-L5
[baseline]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/evidence/release/0.1.0/inventory-4-7.md?plain=1#L357-L368
[qualification]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/evidence/release/0.1.1/README.md?plain=1#L3-L18
[guest]: https://github.com/Benson-mk/tsdm-sdk/blob/dab412339fb8392cead19f3e4b46a5b7255d99cb/evidence/release/0.1.1/guest-read.json#L2-L19
