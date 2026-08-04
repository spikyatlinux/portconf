portconf
========

must be installed from spikyatlinux overlay ONLY!!!
==========================================

/etc/portage cleaner

USE:
        <ul>
        <li>package.use</li>
                <ul>
                        <li>Find and remove incorrect(simple fixes).Checking flags for ALL available versions ( hello, portpeek :3 ).</li>
                        <li>Find and remove flags, which present in make.conf/profile and have the same state.</li>
                        <li>Sort: remove duplicates and preserve only last defined state (on/off).</li>
                        <li>Merge: all flags in one line per atom ("<>=~" switches depend).</li>
                </ul>
        <li>make.conf</li>
                <ul>
                        <li>Find and remove flags, which defined in profile and have the same state.</li>
                </ul>
        </ul>
ATOMS:
        <ul>
                <li>Find and remove incorrect/not_founded/not_installed.( in the /etc/portage/env too ).</li>
        </ul>
Features:
        <ul>
                <li>Auto backup (make.conf/world included).</li>
                <li>Rebuild: package.* from flat files to dirs and back.</li>
                <li>Sort atoms alphabetically</li>
                <li>/etc/portage/make.conf override /etc/make.conf ( as portage ).</li>
        </ul>
Overlays:
        <ul>
                <li>Find and remove unused repos</li>
                <li>Symlink_based ebuilds support</li>
        </ul>
World:
        <ul>
                <li>Regenerate world</li>
        </ul>

---

Rewrites & Fixes by SpikyAtLinux:
=================================

<ul>
<li><b>Full Comment Preservation:</b> Inline-comments and structural headers (like <code># Overlay ...</code>) are now strictly protected. Sorting routines carefully reorganize atoms without destroying manual annotations.</li>
<li><b>Critical Portage Protection:</b> Aggressive trash and empty-file cleaners are now strictly confined to <code>package.*</code> files. Crucial configurations like <code>package.env</code>, <code>env/</code>, <code>gnupg/</code>, and <code>binrepos.conf/</code> are 100% safe from accidental deletion.</li>
<li><b>Enhanced Ignore Logic:</b> The <code>IGNORE_PN</code> and <code>IGNORE_CATEGORY</code> variables in <code>portconf.conf</code> now support multiple, space-separated entries (e.g., <code>IGNORE_PN="dev-lang/php apache dev-lang/rust"</code>) using a modernized, robust regex builder.</li>
<li><b>Profile Directory Protection:</b> Added the <code>-ip</code> (<code>--ignore-profile-dir</code>) flag and <code>IGNORE_PROFILE_DIR</code> config option to safely bypass the entire <code>/etc/portage/profile/</code> directory, protecting local use.mask and use.force overrides.</li>
<li><b>Modern GNU Grep/Sed Compatibility:</b> Resolved all legacy regex syntax errors and warnings (e.g., <code>stray \ before -</code>, invalid wildcards at the start of expressions).</li>
<li><b>Execution Deduplication:</b> Fixed redundant multi-looping. Meta-flags like <code>-f</code> (Full) or <code>-uf</code> (Use-Full) now automatically filter out implied sub-flags to run each check exactly once.</li>
<li><b>Safe make.conf Mode:</b> Multiline bash strings in <code>make.conf</code> (like <code>DESKTOPUSE</code> or <code>HARDWARE_USE</code>) are no longer mangled by destructive <code>sed</code> replacements. The script now performs non-destructive analysis and warns the user about global use flag collisions.</li>
<li><b>Smart Overlay Awareness:</b> Explicitly targeted overlay packages (e.g., <code>cat/pkg::spikyatlinux</code>) in <code>package.unmask</code> are correctly recognized and no longer falsely flagged as "stupid entries".</li>
</ul>
