{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyNiTjqVTc/hxkBo9etR6Kby",
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
        "<a href=\"https://colab.research.google.com/github/kowshik5063/CSA6301-Threat-Intelligence/blob/main/Experiment%2010.md\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "\n",
        "from collections import defaultdict\n",
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
        "\n",
        "def simple_ids(logfile, threshold=3):\n",
        "    attempts = defaultdict(int)\n",
        "    alerts = []\n",
        "\n",
        "    with open(logfile, \"r\") as f:\n",
        "        for line in f:\n",
        "            if \"LOGIN FAILED\" in line:\n",
        "                ip = line.split(\"ip=\")[1].strip()\n",
        "                attempts[ip] += 1\n",
        "\n",
        "                if attempts[ip] == threshold:\n",
        "                    alerts.append(\n",
        "                        f\"IDS ALERT: {threshold}+ failed logins from {ip}\"\n",
        "                    )\n",
        "\n",
        "    return alerts\n",
        "\n",
        "\n",
        "for alert in simple_ids(\"login_attempts.log\", threshold=3):\n",
        "    print(alert)"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "4S_4kE4T-oYy",
        "outputId": "005ffdec-c22a-43ea-bc16-6eca4e979a08"
      },
      "execution_count": 4,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "IDS ALERT: 3+ failed logins from 203.0.113.99\n"
          ]
        }
      ]
    }
  ]
}