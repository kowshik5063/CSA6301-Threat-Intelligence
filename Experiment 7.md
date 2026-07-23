{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyMOARcwsOvmF/iJe5LDNtuQ",
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
      "execution_count": 1,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "JrZ-HswiKloD",
        "outputId": "d4069923-4e8c-45f3-ab73-04c92f4d5400"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "============================================================\n",
            "     INDICATOR OF COMPROMISE (IoC) MATCHING\n",
            "============================================================\n",
            "Loaded 3 IoCs\n",
            "\n",
            "ALERT: Known malicious IP found -> 2026-07-08 10:02:44 connection from 45.33.32.156\n",
            "ALERT: Known malicious IP found -> 2026-07-08 10:04:55 connection from 203.0.113.99\n",
            "\n",
            "Scan Complete!\n"
          ]
        }
      ],
      "source": [
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
        "    with open(filename, \"r\") as file:\n",
        "        return set(line.strip() for line in file if line.strip())\n",
        "\n",
        "def scan_log(logfile, iocs):\n",
        "    with open(logfile, \"r\") as file:\n",
        "        for line in file:\n",
        "            for ip in iocs:\n",
        "                if ip in line:\n",
        "                    print(\"ALERT: Known malicious IP found ->\", line.strip())\n",
        "\n",
        "iocs = load_iocs(\"ioc_list.txt\")\n",
        "\n",
        "print(\"=\" * 60)\n",
        "print(\"     INDICATOR OF COMPROMISE (IoC) MATCHING\")\n",
        "print(\"=\" * 60)\n",
        "\n",
        "print(f\"Loaded {len(iocs)} IoCs\\n\")\n",
        "\n",
        "scan_log(\"sample_traffic.log\", iocs)\n",
        "\n",
        "print(\"\\nScan Complete!\")"
      ]
    },
    {
      "cell_type": "code",
      "source": [
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
        "    with open(filename, \"r\") as file:\n",
        "        return set(line.strip() for line in file if line.strip())\n",
        "\n",
        "def scan_log(logfile, iocs):\n",
        "    with open(logfile, \"r\") as file:\n",
        "        for line in file:\n",
        "            for ip in iocs:\n",
        "                if ip in line:\n",
        "                    print(\"ALERT: Known malicious IP found ->\", line.strip())\n",
        "\n",
        "iocs = load_iocs(\"ioc_list.txt\")\n",
        "\n",
        "print(\"=\" * 60)\n",
        "print(\"     INDICATOR OF COMPROMISE (IoC) MATCHING\")\n",
        "print(\"=\" * 60)\n",
        "\n",
        "print(f\"Loaded {len(iocs)} IoCs\\n\")\n",
        "\n",
        "scan_log(\"sample_traffic.log\", iocs)\n",
        "\n",
        "print(\"\\nScan Complete!\")"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "-WIiWMOLMDxG",
        "outputId": "2bbb4304-f361-4c0b-9b2a-d84b0781fab9"
      },
      "execution_count": 2,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "============================================================\n",
            "     INDICATOR OF COMPROMISE (IoC) MATCHING\n",
            "============================================================\n",
            "Loaded 3 IoCs\n",
            "\n",
            "ALERT: Known malicious IP found -> 2026-07-08 10:02:44 connection from 45.33.32.156\n",
            "ALERT: Known malicious IP found -> 2026-07-08 10:04:55 connection from 203.0.113.99\n",
            "\n",
            "Scan Complete!\n"
          ]
        }
      ]
    }
  ]
}