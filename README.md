<br />

<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/The-PR-Agent/pr-agent/main/docs/static/img/logo-dark.png" width="330">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/The-PR-Agent/pr-agent/main/docs/static/img/logo-light.png" width="330">
  <img src="https://raw.githubusercontent.com/The-PR-Agent/pr-agent/main/docs/static/img/logo-light.png" alt="logo" width="330">
</picture>
<br>
Orijinal Açık Kaynaklı PR İnceleme Aracı
<br><br>
<a href="https://github.com/the-pr-agent/pr-agent/commits/main">
<img alt="GitHub" src="https://img.shields.io/github/last-commit/the-pr-agent/pr-agent/main?style=for-the-badge" height="20">
</a>
</div>

---

Bu depo, açık kaynaklı PR-Agent projesini içerir. Qodo'nun açık kaynak projelere sunduğu ürün değildir.

PR-Agent, yapay zekâ destekli açık kaynaklı bir kod inceleme aracıdır ve Qodo'nun topluluk tarafından sürdürülen eski bir projesidir. Qodo'nun daha kapsamlı özelliklere sahip birincil yapay zekâ kod inceleme ürününden farklıdır.

## Sponsorlar

PR-Agent, geliştirilmesi sponsorlarımızın desteğiyle sürdürülen topluluk odaklı bir açık kaynak projesidir. Projeyi desteklemek isterseniz [sponsor olmayı](https://github.com/sponsors/qodo) değerlendirebilirsiniz.

<p align="center">
  <h3 align="center">🥇 Altın Sponsor</h3>
</p>

<p align="center">
  <a target="_blank" href="https://www.qodo.ai/">
    <img alt="Qodo — Altın sponsor" src="https://www.qodo.ai/wp-content/uploads/2025/03/qodo-logo.svg" width="150">
  </a>
</p>

<p align="center">
  <a target="_blank" href="https://www.qodo.ai/solutions/open-source/">Açık kaynak projeler için Qodo'nun ücretsiz sürümü</a>
</p>

## İçindekiler

- [Başlarken](#başlarken)
- [Neden PR-Agent?](#neden-pr-agent)
- [Özellikler](#özellikler)
- [Kullanım Örneği](#kullanım-örneği)
- [Nasıl Çalışır?](#nasıl-çalışır)
- [Veri Gizliliği](#veri-gizliliği)
- [Katkıda Bulunma](#katkıda-bulunma)

## Başlarken

> [!NOTE]
> **Docker Hub ad alanı değişikliği.** `0.34.2` ve sonraki sürümler [`pragent/pr-agent`](https://hub.docker.com/r/pragent/pr-agent) altında yayımlanır. `v0.31` ve öncesi dahil olmak üzere daha eski sürümler önceki ad alanını kullanır.

### 🚀 PR-Agent için Hızlı Başlangıç

#### 1. GitHub Action (Önerilen)

Basit bir iş akışı dosyasıyla deponuza otomatik PR incelemeleri ekleyin:

```yaml
# .github/workflows/pr-agent.yml
name: PR Agent
on:
  pull_request:
    types: [opened, synchronize]
jobs:
  pr_agent_job:
    runs-on: ubuntu-latest
    steps:
    - name: PR Agent action step
      uses: the-pr-agent/pr-agent@main
      env:
        OPENAI_KEY: ${{ secrets.OPENAI_KEY }}
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
[Tam GitHub Action kurulum kılavuzu](https://docs.pr-agent.ai/installation/github/#run-as-a-github-action)

#### 2. CLI Kullanımı (Yerel Geliştirme)

PR-Agent'i deponuzda yerel olarak çalıştırın:

```bash
pip install "pr-agent[github]"
export OPENAI_KEY=your_key_here
pr-agent --pr_url https://github.com/owner/repo/pull/123 review
```
Git sağlayıcılarının SDK'ları isteğe bağlı ek paketlerdir: kullandığınız sağlayıcıya ait paketi ([liste](https://docs.pr-agent.ai/installation/locally/#using-pip-package)) veya tüm entegrasyonlar için `pr-agent[all]` paketini kurun.
[Tam CLI kurulum kılavuzu](https://docs.pr-agent.ai/usage-guide/automations_and_usage/#local-repo-cli)

#### 3. Diğer Platformlar

- [GitLab webhook kurulumu](https://docs.pr-agent.ai/installation/gitlab/)
- [Bitbucket uygulama kurulumu](https://docs.pr-agent.ai/installation/bitbucket/)
- [Azure DevOps kurulumu](https://docs.pr-agent.ai/installation/azure/)

## Haberler ve Güncellemeler

Her sürümün ayrıntılı notları [Sürümler sayfasında](https://github.com/the-pr-agent/pr-agent/releases) yer alır.

## Neden PR-Agent?

### 🎯 Gerçek Geliştirme Ekipleri için Tasarlandı

**Hızlı ve Ekonomik**: Her araç (`/review`, `/improve`, `/ask`) tek bir LLM çağrısı kullanır (yaklaşık 30 saniye, düşük maliyet).

**Her Boyutta PR'ı İşler**: [PR sıkıştırma stratejimiz](https://docs.pr-agent.ai/core-abilities/compression_strategy/) hem küçük hem de büyük PR'ları etkili şekilde işler.

**Kolayca Özelleştirilebilir**: JSON tabanlı istemler, [yapılandırma dosyaları](pr_agent/settings/configuration.toml) üzerinden inceleme kategorilerini ve davranışını kolayca özelleştirmenizi sağlar.

**Platform Bağımsız**:
- **Git sağlayıcıları**: GitHub, GitLab, Bitbucket, Azure DevOps, Gitea
- **Dağıtım**: CLI, GitHub Actions, Docker, kendi sunucunuzda barındırma, webhook'lar
- **Yapay zekâ modelleri**: OpenAI GPT, Anthropic Claude, Google Gemini, DeepSeek, Mistral ve LiteLLM üzerinden erişilebilen diğer modeller (Azure OpenAI, AWS Bedrock, Vertex AI, Databricks, OpenRouter, Ollama ve daha fazlası)

**Açık Kaynak Avantajları**:
- Verileriniz ve altyapınız üzerinde tam denetim
- İstemleri ve davranışı ekibinizin ihtiyaçlarına göre özelleştirme
- Bir satıcıya bağımlı olmama
- Topluluk odaklı geliştirme

## Özellikler

<div style="text-align:left;">

Güncel [özellik ve Git sağlayıcısı destek matrisini](https://docs.pr-agent.ai/overview/supported_platforms/) PR-Agent belgelerinde görebilirsiniz.

⚠️ `/help_docs`, kimlik bilgilerini açığa çıkarma sorununa yönelik düzeltme beklediği için `v0.36.1` sürümünden bu yana geçici olarak devre dışıdır ([#2445](https://github.com/the-pr-agent/pr-agent/issues/2445)).

[//]: # (- Ek git sağlayıcılarına verilen destek [burada]&#40;./docs/Full_environments.md&#41; açıklanmıştır.)
___

## Kullanım Örneği

</div>
<h4><a href="https://github.com/the-pr-agent/pr-agent/pull/530">/describe</a></h4>
<div align="center">
<p float="center">
<img src="https://raw.githubusercontent.com/The-PR-Agent/pr-agent/main/docs/static/img/describe_new_short_main.png" width="512">
</p>
</div>
<hr>

<h4><a href="https://github.com/the-pr-agent/pr-agent/pull/732#issuecomment-1975099151">/review</a></h4>
<div align="center">
<p float="center">
<kbd>
<img src="https://raw.githubusercontent.com/The-PR-Agent/pr-agent/main/docs/static/img/review_new_short_main.png" width="512">
</kbd>
</p>
</div>
<hr>

<h4><a href="https://github.com/the-pr-agent/pr-agent/pull/732#issuecomment-1975099159">/improve</a></h4>
<div align="center">
<p float="center">
<kbd>
<img src="https://raw.githubusercontent.com/The-PR-Agent/pr-agent/main/docs/static/img/improve_new_short_main.png" width="512">
</kbd>
</p>
</div>

<hr>

### Kullanım Örnekleri

PR-Agent araçlarını bir PR'a yorum olarak ya da CLI üzerinden çalıştırabilirsiniz. Sık kullanılan birkaç örnek:

```bash
# PR üzerinde yorum olarak (GitHub/GitLab/Bitbucket/…):
/describe
/review
/improve
/ask "Bu PR neyi değiştiriyor?" # PR hakkında serbest metinle soru-cevap

# Sorun (issue) kapsamındaki komutlar PR yerine bir issue üzerinde çalışır:
/similar_issue # depodaki benzer issue'ları bul

# Ya da yerel olarak CLI üzerinden:
pr-agent --pr_url <PR_URL> review
pr-agent --issue_url <ISSUE_URL> similar_issue
```

Tüm araçların örnek komutlarla listesi için [Araçlar belgelerine](https://docs.pr-agent.ai/tools/#usage-examples), ekran görüntüleri ve seçenekler için her aracın kendi sayfasına bakın.

<hr>

## Nasıl Çalışır?

Aşağıdaki şema PR-Agent araçlarını ve iş akışlarını gösterir:

![PR-Agent Araçları](https://raw.githubusercontent.com/The-PR-Agent/pr-agent/main/docs/static/img/diagram-v0.9.png)

## Veri Gizliliği

### Kendi Sunucunuzda Barındırılan PR-Agent

- PR-Agent'i kendi OpenAI API anahtarınızla barındırıyorsanız, veriler sizinle OpenAI arasındadır. OpenAI'ın API veri gizliliği politikasını buradan okuyabilirsiniz:
https://openai.com/enterprise-privacy

## Katkıda Bulunma

Projeye katkıda bulunmak için [Katkıda Bulunma Kılavuzu'nu](https://github.com/the-pr-agent/pr-agent/blob/main/CONTRIBUTING.md) okuyarak başlayın.

Yerel doğrulama için deponun kök dizininde `PYTHONPATH=. uv run pytest` komutunu çalıştırın; bu komut varsayılan olarak `tests/unittest` altındaki birim testlerini bulur. `tests/e2e_tests` altındaki uçtan uca testler ortam değişkenleriyle sağlanan kimlik bilgilerini gerektirir.

## PR-Agent için Büyük Haber

PR-Agent'in artık yeni bir yuvası var!

Qodo, yıllarca toplulukla birlikte bu aracı geliştirdikten sonra PR-Agent'i açık kaynak topluluğuna bağışladı. Bundan sonra neler olacağını görmek için heyecanlıyız.

Proje artık GitHub'daki PR-Agent organizasyonunda yer alıyor, tamamen topluluğa ait ve katkılara ve yeni bakım sorumlularına açık.

Diğer değişiklikler:
- Belgeler [docs.pr-agent.ai](https://docs.pr-agent.ai/) adresine taşındı.
- PR-Agent'in kurumsal sürümü olan barındırılan Qodo Merge (Qodo 1.0), yeniden markalandı ve kapsamlı bir yapay zekâ kod inceleme platformu olan Qodo'ya (Qodo 2.0) dönüştü.

## ❤️ Topluluk

Bu açık kaynak sürümü, modern yapay zekâ destekli kod iş birliğinin öncüsü Qodo'nun topluluğa katkısı olarak burada kalmaya devam ediyor. Bunu paylaşmaktan ve dünya çapındaki geliştiricilere ilham vermekten gurur duyuyoruz.

Projenin ilk harici bakım sorumlusu Naor'dur ([@naorpeled](https://github.com/naorpeled)); proje şu anda bir açık kaynak vakfına bağışlanma sürecindedir.
