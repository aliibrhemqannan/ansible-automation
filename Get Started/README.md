# Ansible Inventory Host Listing Commands

Use the following commands to verify your inventory and list hosts.

---

## List All Hosts

```bash
ansible all -i inventory --list-hosts
```

---

## List Hosts in a Specific Group

Replace `<group_name>` with the desired inventory group.

```bash
ansible <group_name> -i inventory --list-hosts
```

**Example:**

```bash
ansible servers -i inventory --list-hosts
```

```bash
ansible production -i inventory --list-hosts
```

---

## List Hosts in the `ungrouped` Group

Display hosts that do not belong to any custom group.

```bash
ansible ungrouped -i inventory --list-hosts
```

---

## List Hosts in the `all` Group

Display every host defined in the inventory.

```bash
ansible all -i inventory --list-hosts
```

---

## Display Inventory as a Tree

Visualize the inventory hierarchy, including groups, child groups, and hosts.

```bash
ansible-inventory -i inventory --graph
```

---

## Display Inventory in YAML Format

```bash
ansible-inventory -i inventory --list --yaml
```

---

## Display Inventory in JSON Format

```bash
ansible-inventory -i inventory --list
```

---

## Verify Inventory Parsing

```bash
ansible-inventory -i inventory --list
```

This command is useful for confirming that Ansible can successfully parse your inventory file.
