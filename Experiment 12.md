{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyMt1usIT2Up/UsZFRNVpkey",
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
        "<a href=\"https://colab.research.google.com/github/kowshik5063/CSA6301-Threat-Intelligence/blob/main/Experiment%2012.md\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "\n",
        "import datetime\n",
        "\n",
        "def generate_report(flagged_ips, source_log):\n",
        "    lines = []\n",
        "\n",
        "    lines.append(\"INCIDENT RESPONSE REPORT\")\n",
        "    lines.append(f\"Generated: {datetime.datetime.now()}\")\n",
        "    lines.append(f\"Source log: {source_log}\")\n",
        "    lines.append(\"-\" * 40)\n",
        "\n",
        "    if flagged_ips:\n",
        "        lines.append(f\"{len(flagged_ips)} suspicious IP(s) detected:\")\n",
        "\n",
        "        for ip, count in flagged_ips.items():\n",
        "            lines.append(f\"- {ip}: {count} failed login attempts\")\n",
        "\n",
        "        lines.append(\n",
        "            \"Recommended action: Block listed IPs, force password reset.\"\n",
        "        )\n",
        "\n",
        "    else:\n",
        "        lines.append(\"No suspicious activity detected.\")\n",
        "\n",
        "    return \"\\n\".join(lines)\n",
        "\n",
        "\n",
        "flagged = {\n",
        "    \"203.0.113.99\": 5\n",
        "}\n",
        "\n",
        "report = generate_report(flagged, \"login_attempts.log\")\n",
        "\n",
        "print(report)\n",
        "\n",
        "with open(\"incident_report.txt\", \"w\") as f:\n",
        "    f.write(report)"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "BSKfdMr1_POj",
        "outputId": "f6d4d336-a409-4fb3-bffc-d709a40c808f"
      },
      "execution_count": 6,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "INCIDENT RESPONSE REPORT\n",
            "Generated: 2026-08-29 05:28:05.682029\n",
            "Source log: login_attempts.log\n",
            "----------------------------------------\n",
            "1 suspicious IP(s) detected:\n",
            "- 203.0.113.99: 5 failed login attempts\n",
            "Recommended action: Block listed IPs, force password reset.\n"
          ]
        }
      ]
    }
  ]
}