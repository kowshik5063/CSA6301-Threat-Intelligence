{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyMnIG1rYb6Z3LU90zO98vuf",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/kowshik5063/CSA6301-Threat-Intelligence/blob/main/Experiment%207.md\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 2,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "BehkGvIJdm-u",
        "outputId": "5ec13359-a63a-41ee-8b2a-c54d6826cfd4"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Loaded 3 IoCs\n",
            "ALERT: Known malicious IP found -> 2026-07-08 10:02:44 connection from 45.33.32.156\n",
            "ALERT: Known malicious IP found -> 2026-07-08 10:04:55 connection from 203.0.113.99\n"
          ]
        }
      ],
      "source": [
        "\n",
        "with open(\"ioc_list.txt\", \"w\") as f:\n",
        "    f.write(\"45.33.32.156\\n\")\n",
        "    f.write(\"198.51.100.23\\n\")\n",
        "    f.write(\"203.0.113.99\\n\")\n",
        "\n",
        "with open(\"sample_traffic.log\", \"w\") as f:\n",
        "    f.write(\"2026-07-08 10:01:12 connection from 10.0.0.5\\n\")\n",
        "    f.write(\"2026-07-08 10:02:44 connection from 45.33.32.156\\n\")\n",
        "    f.write(\"2026-07-08 10:03:10 connection from 192.168.1.20\\n\")\n",
        "    f.write(\"2026-07-08 10:04:55 connection from 203.0.113.99\\n\")\n",
        "\n",
        "def load_iocs(filename):\n",
        "    with open(filename, \"r\") as f:\n",
        "        return set(line.strip() for line in f if line.strip())\n",
        "\n",
        "def scan_log(logfile, iocs):\n",
        "    with open(logfile, \"r\") as f:\n",
        "        for line in f:\n",
        "            for ip in iocs:\n",
        "                if ip in line:\n",
        "                    print(\"ALERT: Known malicious IP found ->\", line.strip())\n",
        "\n",
        "iocs = load_iocs(\"ioc_list.txt\")\n",
        "\n",
        "print(\"Loaded\", len(iocs), \"IoCs\")\n",
        "scan_log(\"sample_traffic.log\", iocs)"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "# Experiment 7: Log File Analyzer\n",
        "\n",
        "import re\n",
        "from collections import Counter\n",
        "\n",
        "# Step 1: Create the sample login log file\n",
        "with open(\"login_attempts.log\", \"w\") as f:\n",
        "    f.write(\"2026-07-08 09:00:01 LOGIN SUCCESS user=alice ip=10.0.0.5\\n\")\n",
        "    f.write(\"2026-07-08 09:01:15 LOGIN FAILED user=admin ip=203.0.113.99\\n\")\n",
        "    f.write(\"2026-07-08 09:01:20 LOGIN FAILED user=admin ip=203.0.113.99\\n\")\n",
        "    f.write(\"2026-07-08 09:01:25 LOGIN FAILED user=admin ip=203.0.113.99\\n\")\n",
        "    f.write(\"2026-07-08 09:01:30 LOGIN FAILED user=admin ip=203.0.113.99\\n\")\n",
        "    f.write(\"2026-07-08 09:01:35 LOGIN FAILED user=admin ip=203.0.113.99\\n\")\n",
        "    f.write(\"2026-07-08 09:02:00 LOGIN SUCCESS user=bob ip=10.0.0.8\\n\")\n",
        "\n",
        "# Step 2: Count failed login attempts\n",
        "failed_by_ip = Counter()\n",
        "\n",
        "with open(\"login_attempts.log\", \"r\") as f:\n",
        "    for line in f:\n",
        "        if \"LOGIN FAILED\" in line:\n",
        "            match = re.search(r\"ip=(\\S+)\", line)\n",
        "\n",
        "            if match:\n",
        "                ip = match.group(1)\n",
        "                failed_by_ip[ip] += 1\n",
        "\n",
        "# Step 3: Display results\n",
        "print(\"Failed login attempts by IP:\")\n",
        "\n",
        "for ip, count in failed_by_ip.items():\n",
        "    print(f\"{ip}: {count} attempts\")\n",
        "\n",
        "    if count >= 5:\n",
        "        print(f\"-> ALERT: possible brute-force attack from {ip}\")"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "uPxLwg8biIOA",
        "outputId": "051ed02b-5134-4cd5-d0b0-6c6d3ca2d612"
      },
      "execution_count": 3,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Failed login attempts by IP:\n",
            "203.0.113.99: 5 attempts\n",
            "-> ALERT: possible brute-force attack from 203.0.113.99\n"
          ]
        }
      ]
    }
  ]
}