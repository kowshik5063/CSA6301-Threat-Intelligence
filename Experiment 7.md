{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyOANtm0bCA4iRjcIK9Oydow",
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
      "source": [
        "\n",
        "import re\n",
        "from collections import Counter\n",
        "\n",
        "with open(\"login_attempts.log\", \"w\") as f:\n",
        "    f.write(\"2026-07-08 09:00:01 LOGIN SUCCESS user=alice ip=10.0.0.5\\n\")\n",
        "    f.write(\"2026-07-08 09:01:15 LOGIN FAILED user=admin ip=203.0.113.99\\n\")\n",
        "    f.write(\"2026-07-08 09:01:20 LOGIN FAILED user=admin ip=203.0.113.99\\n\")\n",
        "    f.write(\"2026-07-08 09:01:25 LOGIN FAILED user=admin ip=203.0.113.99\\n\")\n",
        "    f.write(\"2026-07-08 09:01:30 LOGIN FAILED user=admin ip=203.0.113.99\\n\")\n",
        "    f.write(\"2026-07-08 09:01:35 LOGIN FAILED user=admin ip=203.0.113.99\\n\")\n",
        "    f.write(\"2026-07-08 09:02:00 LOGIN SUCCESS user=bob ip=10.0.0.8\\n\")\n",
        "\n",
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
        "\n",
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